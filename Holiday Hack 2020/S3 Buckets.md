## Intro
- Cloud storage mechaninsm 
- similar to local file storage system
- Previously by default had public access (later Amazon fixed that)

## Buckets

- Bucket Id and ARN (Amazon Resource Number)
- arn:aws:s3::bucketname
- Bucket name chosen by user (globally unique)
- Commonly Can be accessed using http or https
- Eg,  https://s3.amazonaws.com/bucketname (s3 region code are used for region-specifilc)

## HOw to find these resources

- Buckt_finder (Robin wood) uses wordlist 
	- `./bucket_finder.rb wordlist --download`
	- wordlist dependent (your creativity)
- https://buckets.grayhatwarfarefree.com 


## Defenses

- Scan your own organization
- Use logs (DNS, proxy logs, EDR reports etc)
- 