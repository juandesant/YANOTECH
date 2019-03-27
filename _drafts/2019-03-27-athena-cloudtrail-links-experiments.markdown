---
layout: post
title:  "Relevant links and experiments with AWS Athena and CloudTrail"
date:   2019-03-27 00:00:00 -0300
categories: aws, cloud, monitoring 
---

If you're trying to investigate what operation gave birth to a given Amazon Web Services (AWS) resource, specially one that you will pay for, but are not sure if it is worth paying for, the best way to investigate about it is using [AWS CloudTrail][AWS_CloudTrail].

[AWS_CloudTrail]: https://aws.amazon.com/cloudtrail/ "AWS CloudTrail – Amazon Web Services"

However, the query abilities of CloudTrail are not that big, and most of the time you will want to dig into them, in particular if you want to make use of things like resource names, or [Amazon Resource Names][ARNs] (ARNs). 

[ARNs]: https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html "Amazon Resource Names (ARNs) and AWS Service Namespaces - Amazon Web Services"

While I complete the post, here is a list of links, and relevant code that I find useful:

 * Athena: Querying AWS CloudTrail Logs: [https://docs.aws.amazon.com/athena/latest/ug/cloudtrail-logs.html](https://docs.aws.amazon.com/athena/latest/ug/cloudtrail-logs.html "Querying AWS CloudTrail Logs - Amazon Athena")
 * Athena: Extracting JSON data: [https://docs.aws.amazon.com/athena/latest/ug/querying-JSON.html](https://docs.aws.amazon.com/athena/latest/ug/querying-JSON.html "Querying JSON - Amazon Athena")
 * Analyzing CloudTrail with Athena, by Andreas Wittig: [https://cloudonaut.io/analyzing-cloudtrail-with-athena/](https://cloudonaut.io/analyzing-cloudtrail-with-athena/ "cloudonaut: Analyzing CloudTrail with Athena")
 
And this is a query that is successful in retrieving resource names for those items that include resource names:

    SELECT uarn,
             eventname,
             sourceipaddress,
             eventtime,
             resources[1].arn as res_arn
    FROM 
        (SELECT useridentity.arn AS uarn,
             eventname,
             sourceipaddress,
             eventtime,
             resources
        FROM cloudtrail_logs_aws_cloudtrail_do_pocops
        WHERE readonly = 'false'
                AND cardinality(resources) >= 1 ) AS t 
    WHERE resources[1].arn like '%resource_id%'
    LIMIT 100;

I'll keep ellaborating this draft.