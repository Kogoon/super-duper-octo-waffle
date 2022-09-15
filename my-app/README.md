## project
`brokurly-eks-cluster`

* Route53
~~~
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "route53:ChangeResourceRecordSets"
      ],
      "Resource": [
        "arn:aws:route53:::hostedzone/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "route53:ListHostedZones",
        "route53:ListResourceRecordSets"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
~~~

~~~
eksctl create iamserviceaccount --name external-dns --cluster brokurly-eks-cluster --attach-policy-arn arn:aws:iam::709861978753:policy/External-DNS-ROUTE53-ROLE --approve
~~~