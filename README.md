# leetcode

uses GitHub actions to automatically upload completed solutions to gulkaran.ca/leetcode.

- dynamoDB table is modeled after github repo
- s3 buckets to hold .md files which are displayed on gulkaran.ca/leetcode
- both s3 and dynamoDB are updated with every commit through the GitHub Actions workflow

## process of completing LC questions

1. Write notes in Notion (export as .md)
2. Add and commit .md file to the GitHub repo
3. GitHub Action workflow transforms the .md file
4. Adds .md file to S3 bucket
5. Adds entry into DynamoDB Table
6. Leetcode question is now viewable on gulkaran.ca/leetcode
