# Terraforming

[![Build Status](https://travis-ci.org/dtan4/terraforming.svg?branch=master)](https://travis-ci.org/dtan4/terraforming)
[![Code Climate](https://codeclimate.com/github/dtan4/terraforming/badges/gpa.svg)](https://codeclimate.com/github/dtan4/terraforming)
[![Test Coverage](https://codeclimate.com/github/dtan4/terraforming/badges/coverage.svg)](https://codeclimate.com/github/dtan4/terraforming)

Import existing AWS resources into [Terraform](https://terraform.io/) style (tf, tfstate)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'terraforming'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install terraforming

## Prerequisites

You need to set AWS credentials.

```bash
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
```

## Usage

```bash
$ terraforming
Commands:
  terraforming dbpg            # Database Parameter Group
  terraforming dbsg            # Database Security Group
  terraforming dbsn            # Database Subnet Group
  terraforming ec2             # EC2
  terraforming elb             # ELB
  terraforming help [COMMAND]  # Describe available commands or one specific command
  terraforming nacl            # Network ACL
  terraforming rds             # RDS
  terraforming s3              # S3
  terraforming sg              # SecurityGroup
  terraforming sn              # Subnet
  terraforming vpc             # VPC
```

Output `.tf` style (e.g. S3 buckets):

```bash
$ terraforming s3
```

```go
resource "aws_s3_bucket" "hoge" {
    bucket = "hoge"
    acl    = "private"
}

resource "aws_s3_bucket" "fuga" {
    bucket = "fuga"
    acl    = "private"
}
```

To output `.tfstate` style, specify `--tfstate` option (e.g. S3 buckets):

```bash
$ terraforming s3 --tfstate
```

```json
{
  "version": 1,
  "serial": 1,
  "modules": {
    "path": [
      "root"
    ],
    "outputs": {
    },
    "resources": {
      "aws_s3_bucket.hoge": {
        "type": "aws_s3_bucket",
        "primary": {
          "id": "hoge",
          "attributes": {
            "acl": "private",
            "bucket": "hoge",
            "id": "hoge"
          }
        }
      },
      "aws_s3_bucket.fuga": {
        "type": "aws_s3_bucket",
        "primary": {
          "id": "fuga",
          "attributes": {
            "acl": "private",
            "bucket": "fuga",
            "id": "fuga"
          }
        }
      }
    }
  }
}
```

(Probably you have to modify the output to add it to existing `terraforming.tfstate`)

## Development

After checking out the repo, run `scripts/setup` to install dependencies. Then, run `scripts/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/dtan4/terraforming/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## LICENSE

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)
