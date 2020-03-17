# @purple/serverless-s3-remover

Plugin for serverless to make buckets empty before remove.

## Original project

[Original project](https://github.com/sinofseven/serverless-s3-remover) is not
maintained anymore, so we published this version under `@purple` organisation.

Main difference between [`serverless-s3-remover`](https://www.npmjs.com/package/serverless-s3-remover) and [`@purple/serverless-s3-remover`](https://www.npmjs.com/package/@purple/serverless-s3-remover)
is ability to empty buckets with enabled versioning.

[`serverless-s3-remover`](https://www.npmjs.com/package/serverless-s3-remover) is not able to empty buckets with enabled versioning.

# Usage

Run next command.

```bash
$ npm install @purple/serverless-s3-remover
```

Add to your serverless.yml

```yaml
plugins:
  - "@purple/serverless-s3-remover"

custom:
  remover:
    buckets:
      - my-bucket-1
      - my-bucket-2
```

You can specify any number of `bucket`s that you want.

Now you can make all buckets empty by running:

```bash
$ sls s3remove
```

# When removing

When removing serverless stack, this plugin automatically make buckets empty before removing stack.

```sh
$ sls remove
```

# Using Prompt

You can use prompt before deleting bucket.

```yaml
custom:
  remover:
    prompt: true # default value is `false`
    buckets:
      - remover-bucket-a
      - remover-bucket-b
```

![terminal.png](https://user-images.githubusercontent.com/57114/31264298-0896f1ec-aaa3-11e7-9a8e-86e3c3f34e23.png)

# Populating the configuration object before using it

```yaml
custom:
  boolean:
    true: true
    false: false
  remover:
    prompt: ${self:custom.boolean.${opt:s3-remover-prompt, 'true'}}
```

I can use the command line argument `--s3-remover-prompt false` to disable the prompt feature.
