# ⚡️ Serverless Plugin to sync content to S3 Buckets

A [Serverless Framework](https://serverless.com) plugin to sync contents of local directories to one or more S3 buckets.

## Features

The `serverless-sync-s3buckets` plugin supports the following:
- Synchronize contents of local directories to __more than one__ s3 bucket.
- Use the __resource reference__ of an s3 buckets whose name is dynamically generated by cloudformation at deploy time.
- __Use commands__ to sync and remove content from s3 buckets without needing to deploy again.
- Display basic information about your s3 buckets in your cloudformation stack.

## Installation

Add the [NPM package](https://www.npmjs.com/package/serverless-sync-s3buckets) to your project:

```sh
$ npm install --save serverless-sync-s3buckets
```

Add the plugin to your `serverless.yml` file

```yaml
plugins:
  - serverless-sync-s3buckets
```

## Configuration
To configure operations in your `serverless.yml`, add references to your local folder and the name of the S3 bucket as follows:

```yaml
custom:
  # Used by the serverless plugin to sync files to S3
  syncS3Buckets:
    - bucketName: my-static-assets # required
      bucketPrefix: assets/        # optional
      localDir: dist/assets        # required
    - bucketRef: WebSiteBucket     # Reference resource whose name is dynamically generated
      localDir: path/to/web-site
      
resources:
  Resources:
    AssetsBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: my-static-assets
    WebSiteBucket:
      Type: AWS::S3::Bucket
      Properties:
        AccessControl: PublicRead
        WebsiteConfiguration:
          IndexDocument: index.html
          ErrorDocument: error.html
```

## Usage

Run `serverless deploy`, to sync specified local directories to their s3 buckets and display s3 information.

Run `serverless s3info`, to display information in cloudformation stack on s3 buckets.

Run `serverless syncToS3`, to sync specified local directories to their s3 buckets.

Run `serverless deleteFromS3`, to remove content from s3 buckets.

Per request, the plugin does NOT remove content from the s3 buckets when you run `serverless remove`.

# Releases

- August 2017 - initial release with full lifecycle support for s3 buckets.

## License

Feel free to use the code, it's released using the [MIT license](LICENSE.md).