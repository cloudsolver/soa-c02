#Q How does X-Ray work to provide tracing?
See: [Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)
**Answer**: Applications need to be instrumented with the X-Ray SDK that supports various languages. Trace data in JSON-snippet is sent to the X-Ray daemon over UDP. [[EC2]] instances must have the daemon installed and running and [[IAM]] role has proper permissions e.g. `AWSXRayDaemonWriteAccess` includes permission to upload traces. For Lambda, ensure it has an IAM execution role with proper policy.
![[X-Ray Architecture.png]]
Fig. X-Ray Architecture

#Q How can you limit the results based on keys or custom attributes? 
See:
![[X-Ray Trace Filter.png]]
Fig. X-Ray Trace Filter
Answer: Add annotations in your segment document. Unlike meta-data, these are indexed.

#Q What are the key concepts of X-Ray ?
See: Developer Guide
Answer:
AWS X-Ray receives data from services as segments. X-Ray then groups segments that have a common request into traces. X-Ray processes the traces to generate a service graph that provides a visual representation of your application.

| Concept     | Description |
| ----------- | ---------- |
| Segment     |  The compute resources running your application logic send data about their work as segments. A segment provides the resource's name, details about the request, and details about the work done.           |
| Sub-Segment |  A segment can break down the data about the work done into subsegments. Subsegments provide more granular timing information and details about downstream calls that your application made to fulfill the original request.          |
| Trace       |  A trace ID tracks the path of a request through your application. A trace collects all the segments generated by a single request.          |
| Annotation  |Annotations are simple key-value pairs that are indexed for use with filter expressions (p. 53). Use annotations to record data that you want to use to group traces in the console, or when calling the GetTraceSummaries API.            |
| Metadata            | Metadata are key-value pairs with values of any type, including objects and lists, but that are not indexed. Use metadata to record data you want to store in the trace but don't need to use for searching traces.           |
