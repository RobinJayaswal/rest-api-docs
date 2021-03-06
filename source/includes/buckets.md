# Buckets


## Add Bucket


> Definition

```bash
POST https://api.cosmicjs.com/v1/buckets
```

```javascript
Cosmic.addBucket()
```

> Example Request

```bash
curl -X POST "https://api.cosmicjs.com/v1/buckets" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV..." \
-H "Content-Type: application/json" \
-d '{"title": "My New Bucket"}'
```

```javascript
const Cosmic = require('cosmicjs')({
  token: 'your-token-from-auth-request' // required
})
Cosmic.addBucket({
  title: 'My New Bucket',
  slug: 'my-new-bucket' // must be unique across all Buckets in system
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "my-new-bucket",
    "title": "My New Bucket"
  }
}
```

`title` is the only required property.  If no `slug` is present, the title will be <a href="https://www.npmjs.com/package/url-slug" target="_blank">converted to a slug</a>.  See the table below for the other optional properties.  The Bucket request matches the `bucket.json` file located in Your Bucket Dashboard > Import Export.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | required | String | Your Bucket title
slug |  | String | <a href="https://www.npmjs.com/package/url-slug" target="_blank">URL-friendly</a> unique identifier
read_key |  | String | Restrict read access
write_key |  | String | Restrict write access
cluster |  | String | Add this Bucket to a Cluster.  ID of existing Cluster
object_types |  | Array | Populate your Bucket with Object Types.  See <a href="#object-types">Object Types</a> for model.
objects |  | Array | Populate your Bucket with Objects. See <a href="#objects">Objects</a> for model.
media |  | Array | Populate your Bucket with Media. See <a href="#media">Media</a> for model.
media_folders |  | Array | Populate your Bucket with Media Folders. See <a href="#media">Media</a> for model.
webhooks |  | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks</a>. See <a href="#webhooks">Webhooks</a> for model.
extensions |  | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions</a>. See <a href="#extensions">Extensions</a> for model.

## Connect to Bucket

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site"
```

```javascript
// Use the Cosmic.bucket method to connect to different Buckets in your account.
const Cosmic = require('cosmicjs')({
  token: 'your-token-from-auth-request' // optional
})
const bucket = Cosmic.bucket({
  slug: 'my-first-bucket',
  read_key: '',
  write_key: ''
})
const bucket2 = Cosmic.bucket({
  slug: 'my-other-bucket',
  read_key: '',
  write_key: ''
})
```

For the NPM module:

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
slug | required | String | The Bucket slug
read_key |  | String | Restrict read access
write_key |  | String | Restrict write access

## Get Bucket

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket_slug
```

```javascript
bucket.getBucket()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site"
```

<script src="https://embed.runkit.com" data-element-id="runkit-get-bucket"></script>
<pre class="runkit" id="runkit-get-bucket">
const Cosmic = require('cosmicjs')
const api = Cosmic()
const bucket = api.bucket({
  slug: 'wedding-site'
})
bucket.getBucket().then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
</pre>


Returns the entire Bucket including Object Types, Objects, Media and more.  If you would like to restrict read access to your Bucket, you can do so in Your Bucket > Basic Settings.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
hide_metafields |  | Enum | true, Hides metafields
read_key |  | String | Restrict read access to your Bucket



## Delete Bucket

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/buckets/:bucket_id
```

```javascript
Cosmic.deleteBucket()
```

> Example Request

```bash
DELETE https://api.cosmicjs.com/v1/buckets/:bucket_id
```

```javascript
const Cosmic = require('cosmicjs')){
  token: 'your-token-from-auth-request' // required
})
Cosmic.deleteBucket({
  id: 'bucket_id'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "status": "200",
  "message": "Bucket deleted"
}
```


Delete an existing Object in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | required | String | The Bucket id found as "_id"
token | required | String | You can only delete Buckets that you have created / own.