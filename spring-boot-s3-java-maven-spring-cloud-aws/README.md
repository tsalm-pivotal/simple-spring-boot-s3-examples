Simple S3 sample using Spring Cloud AWS
============

This is a example application for using AWS S3 with [Spring Boot](http://projects.spring.io/spring-boot/),
[Spring Cloud AWS](https://cloud.spring.io/spring-cloud-aws/reference/html/), Java and Maven.

*Hint: The configuration of the endpoint for the AWS S3 client is currently not supported by 
[Spring Cloud AWS](https://cloud.spring.io/spring-cloud-aws/reference/html/). 
So S3 compatible Storage is not supported!
See https://github.com/spring-cloud/spring-cloud-aws/issues/333*

## Running the application locally
1. Clone the repository and move to the project folder.
    ```
    $ git clone https://github.com/tsalm-pivotal/simple-spring-boot-s3-examples
    $ cd simple-spring-boot-s3-examples/spring-boot-s3-java-maven-spring-cloud-aws
    ```
2. Open the application.yml file in src/main/resources and replace the placeholder values with those appropriate for your environment.
    ```
    cloud.aws:
      credentials:
        accessKey: YOUR_ACCESS_KEY
        secretKey: YOUR_SECRET_KEY
      region:
        static: eu-central-1
      stack:
        auto: false
    ```
3. Run the application.
    ```
    $ ./mvnw spring-boot:run
    ```
4. Call the API.
    - Upload a file to an existing bucket in the configured region:
        ```
            $curl -F "data=@/YOUR/PATH/TO/FILE.txt" http://localhost:8080/api/v1/buckets/YOUR_BUCKET_NAME/objects -v
        ```
    - Download an existing file from a bucket in the configured region:
        ```
            $curl -O http://localhost:8080/api/v1/buckets/YOUR_BUCKET_NAME/objects/FILE.txt -v
        ```
    - Delete an existing file from a bucket in the configured region:
        ```
            $curl -X "DELETE" http://localhost:8080/api/v1/buckets/YOUR_BUCKET_NAME/objects/FILE.txt -v
        ```