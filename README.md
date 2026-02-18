# Component Crawler

http://component-crawler.herokuapp.com/

Crawl github users for components. Only works with Chrome right now due to a lack of vendor prefixing.

Some notes:

- It skips `component.json`s with `private: true`.
- It skips repositories with issues disabled.
- It tries to skip bare repositories, but sometimes fails.
- The `.version` could be wrong if not updated correctly (the crawler only checks `master`).
- GitHub data is added as `.github` to each `component.json`.
- Watcher counts are not included because GitHub's search API does not include that field.

## API

### GET /.json

Returns an object:

- `users` - an object of all the users crawled.
- `components` - array of `component.json`s.

### GET /log

Return an event source stream of updates.

### GET /:user

Return all a user's components.

### PATCH /:user

Update all the components of a user.

### GET /:user/:repo

Return a repo's `component.json`.


## Development

### Setup

- create an AWS [S3](http://aws.amazon.com/en/s3/) bucket in the __US Standard__ region
- create an AWS [IAM](http://aws.amazon.com/en/iam/) user 
  - copy the ACCESS KEY and the SECRET
  - apply the __AmazonS3FullAccess__ policy to the user
- run these commands in your terminal:

```
export S3_KEY='<YOUR_KEY>'
export S3_SECRET='<YOUR_SECRET>'
export S3_BUCKET='<YOUR_BUCKET_NAME>'
```

### Test

`npm test`

### Start the app

`npm start` then open `localhost:3000` in your browser.
At the `localhost:3000/` you can type in a github username or organisation at the bottom and
after a while you can see the result at `localhost:3000/.json`

