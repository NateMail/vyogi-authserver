### REMINDERS
   Fire up mongod like:
   ```
   mongod --dbpath=/path/to/mongopackage
   (stop forgetting where this is...)
   ```

   Good script:
   ```
   var getAllIds = db.getCollection('x').find({}, {_id:1}).map(function(item){ return item._id; })
   ```

   For big file seeding (mongo shell):
   ```
   var file = cat('./schemas/lessons/Sat\ Jan\ 30\ 2021\ 15:00:44\ GMT-0500\ \(Eastern\ Standard\ Time\).json');

   var o = JSON.parse(file);

   db.lessons.insert(o);

   db.lessons.save()
   ```

   Something like this will update a nested array that already has at least one entry. $push is a very cool command, because you can also attach nested attrs to a document on the fly i.e a custom attr.  
   ```
   User.update({"email": "client1@clientmail.com"}, {$push: {bookings: {bookingId: "bkg", lessonId: "lsn"}}});

   User.update({"email": "client1@clientmail.com"}, {$push: {friends: {bookingId: "bkg", lessonId: "lsn"}}});
   ```

   Something like this will update a nested array that doesn't have an entries
   ```
   User.update({"email": "client1@clientmail.com"}, {$addToSet: {bookings: {bookingId: "bkg", lessonId: "lsn"}}});
   ```
   Good thing to have around when dealing with time in the backend 
   ```
   new Date(1612066842332).toLocaleString('en-US', { timeZone: 'America/New_York' })
   ```

   From the Amazon docs, all possible bucket params on putObject operation
   https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#putObject-property
   ```
   var params = {
     Bucket: 'STRING_VALUE', /* required */
     Key: 'STRING_VALUE', /* required */
     ACL: private | public-read | public-read-write | authenticated-read | aws-exec-read | bucket-owner-read | bucket-owner-full-control,
     Body: Buffer.from('...') || 'STRING_VALUE' || streamObject,
     BucketKeyEnabled: true || false,
     CacheControl: 'STRING_VALUE',
     ContentDisposition: 'STRING_VALUE',
     ContentEncoding: 'STRING_VALUE',
     ContentLanguage: 'STRING_VALUE',
     ContentLength: 'NUMBER_VALUE',
     ContentMD5: 'STRING_VALUE',
     ContentType: 'STRING_VALUE',
     ExpectedBucketOwner: 'STRING_VALUE',
     Expires: new Date || 'Wed Dec 31 1969 16:00:00 GMT-0800 (PST)' || 123456789,
     GrantFullControl: 'STRING_VALUE',
     GrantRead: 'STRING_VALUE',
     GrantReadACP: 'STRING_VALUE',
     GrantWriteACP: 'STRING_VALUE',
     Metadata: {
       '<MetadataKey>': 'STRING_VALUE',
       /* '<MetadataKey>': ... */
     },
     ObjectLockLegalHoldStatus: ON | OFF,
     ObjectLockMode: GOVERNANCE | COMPLIANCE,
     ObjectLockRetainUntilDate: new Date || 'Wed Dec 31 1969 16:00:00 GMT-0800 (PST)' || 123456789,
     RequestPayer: requester,
     SSECustomerAlgorithm: 'STRING_VALUE',
     SSECustomerKey: Buffer.from('...') || 'STRING_VALUE' /* Strings will be Base-64 encoded on your behalf */,
     SSECustomerKeyMD5: 'STRING_VALUE',
     SSEKMSEncryptionContext: 'STRING_VALUE',
     SSEKMSKeyId: 'STRING_VALUE',
     ServerSideEncryption: AES256 | aws:kms,
     StorageClass: STANDARD | REDUCED_REDUNDANCY | STANDARD_IA | ONEZONE_IA | INTELLIGENT_TIERING | GLACIER | DEEP_ARCHIVE | OUTPOSTS,
     Tagging: 'STRING_VALUE',
     WebsiteRedirectLocation: 'STRING_VALUE'
   };
   s3.putObject(params, function(err, data) {
     if (err) console.log(err, err.stack); // an error occurred
     else     console.log(data);           // successful response
   });
``` 

   https://docs.mongodb.com/manual/reference/operator/update/pull/