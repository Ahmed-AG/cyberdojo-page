---
layout: post
title:  "Installing to CDF"
date:   2022-07-20 19:21:48 -0500
categories: CDF
---
## Requirements
You will need the following on your local machine:
1. Python3
2. awscli
3. cdk: run the Bootstrapping process four at https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html
```bash
cdk bootstrap aws://ACCOUNT-NUMBER-1/REGION-1
```
4. docker

## Configurationt
 1. Clone the repo
 2. Rename `config.d.templates` to `config.d`
 3. Edit `config.d/config.json` to set pipelines names, sources, deployment options, and any parameters needed

Sample config.json file:

```bash
{
    "pipelines" :[
        {
            "name" : "Production-Pipeline1",
            "provider" : "aws",
            "source" : {
                "source_type" : "codecommit",
                "repo_name" : "cdf-repo1",
                "branch" : "main"
            },
            "deployment" : {
                "assume_role" :{
                    "role": "TODO"
                },
                "aws_account" : "",
                "iam_policy_file" : "config.d/iam-policy.json",
                "region" : "us-east-1",
                "type" : "cfn",
                "parameters" : "VpcCIDR=10.0.0.0/16 Region=$REGION",
                "capabilities" : "CAPABILITY_IAM CAPABILITY_NAMED_IAM",
                "deployment_file" : "main.yaml",
                "checks" : [
                    "general_all",
                    "cfn_nag", 
                    "checkov"
                ]
            }
        }
    ]
}
```
4. Edit the IAM policy file used by the pipeline to deploy resources `config.d/iam-policy.json`
   Note: This file is referenced in `config.d/config.json`. It is recomended to have different policies for each pipeline

5. Run:
```bash
cdk deploy --all
```
6. Verify that your pipelines were created in Codepipline in AWS console

<!-- You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/ -->
