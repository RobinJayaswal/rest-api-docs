# Buckets


## Add Bucket
`title` is the only required property.  See the table below for the other optional properties.  The Bucket request matches the `bucket.json` file located in Your Bucket Dashboard > Import Export.


> Definition

```bash
POST https://api.cosmicjs.com/v1/buckets
```

```javascript
Cosmic.addBucket()
```

> Example Request

```bash
curl -X POST https://api.cosmicjs.com/v1/buckets \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U" \
-H "Content-Type: application/json" \
-d '{"title": "My New Bucket"}'
```

```javascript
const response = await Cosmic.addBucket({ title: "My New Bucket" });
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

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | true | String | Your Bucket title
slug | false | String | URL-friendly unique identifier
read_key | false | String | Restrict read access
write_key | false | String | Restrict write access
object_types | false | Array | Populate your Bucket with Object Types.  See <a href="/#object-types">Object Types</a> for model.
objects | false | Array | Populate your Bucket with Objects. See <a href="/#objects">Objects</a> for model.
media | false | Array | Populate your Bucket with Media. See <a href="/#media">Media</a> for model.
media_folders | false | Array | Populate your Bucket with Media Folders. See <a href="/#media">Media</a> for model.
webhooks | false | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks</a>. See <a href="/#webhooks">Webhooks</a> for model.
extensions | false | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions</a>. See <a href="/#extensions">Extensions</a> for model.


## Get Bucket

> Definition

```json
GET https://api.cosmicjs.com/:bucket-slug
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site"
```

```javascript
const Cosmic = require('cosmicjs');
const api = Cosmic.config({
  bucket: 'test-bucket',
  read_key: '1234asdf'
});
const response = await api.getBucket();
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "wedding-site",
    "title": "Wedding Site",
    "object_types": [
      ...
    ],
    "links": [
      ...
    ],
    "objects": [
      ...
    ],
    "media": [
      ...
    ],
    "media_folders": [
      ...
    ]
  }
}
```


Returns the entire Bucket.  If you would like to restrict read access to your Bucket, you can do so in Your Bucket > Basic Settings.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
hide_metafields | false | Enum | true, Hides metafields
read_key | false | String | Restrict read access to your Bucket