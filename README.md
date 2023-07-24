# Learn-Terraform-with-Google-Cloud-Platform-Infrastructure-as-Code-Course

https://www.youtube.com/watch?v=VCayKl82Lt8 





Deploy an website to google cloud platform using terraform

Users
Cloud DNS ( Domain Name System )
Cloud CDN ( Content Distribution Network )
Cloud load Balancing 
Cloud storage 

Google Cloud Platform
Terraform 
Domain Name
GCloud 

Google Cloud
Select a project
Name                  ID
Youtube               lateral academy-31813

Cloud DNS API
Compute Engine API ( Load Balancer )
IAM API

Quick access 
APIs and services
Enable APIs and services
Welcome to the API library
Cloud DNS API
Manage
Compute Engine API
Manage
IAM API
Enable

IAM and admin
Service accounts 
Create a service account
Service account details
Service account name
freecodecamp-terraform
Service account ID
freecodecamp-terraform
Service account description 
Terraform with GCP
Create and continue 
Grant this service account access to the project
Quick access
Basic
Select a role
Owner
Done
Service accounts for project “Youtube”
Email
freecodecamp-terraform@lateral–academy
Keys
Add key
Create new key
Key type JSON
Create

Install Terraform 
https://brew.sh/
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli#install-cli 

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
main.tf

main.tf
# GCP provider

provider "google" {
  credentials  = file(var.gcp_svc_key)
  project      = var.gcp_project
  region       = var.gcp_region
}

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
main.tf

main.tf
# Bucket to store website
resource "google_storage_bucket" "website" {
  provider = google
  name     = "example-rishab-coffee7"
  location = "US"
}

# Make new objects public
resource "google_storage_object_access_control" "public_rule" {
  object = google_storage_bucket_object.static_site_src.output_name
  bucket = google_storage_bucket.website.name
  role   = "READER"
  entity = "allUsers"
}

# Upload the html file to the bucket
resource "google_storage_bucket_object" "static_site_src" {
  name   = "index.html"
  source = "../website/index.html"
  bucket = google_storage_bucket.website.name
  
}

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
.terraform.lock.hcl

.terraform.lock.hcl
# This file is maintained automatically by "terraform init".
# Manual edits may be lost in future updates.

provider "registry.terraform.io/hashicorp/google" {
  version = "4.63.1"
  hashes = [
    "h1:AJ0z+BKwPr0rEBmfRiIt3RhFKDlCZrlc/mVGPUdsJTw=",
    "zh:0c8e024715dfe8bb4837059fc1a32369bf83f445129ebd3511591650eb9b3961",
    "zh:3ca839141b59d670cc04a3f918fbbb3c6c95eeb8215bbb4214d1a2a57d1f6f7d",
    "zh:3f68f83aaeecaf05f1066d0c7ca23ebc959a1ed10c57fd9f4d958b6b8d38fcc2",
    "zh:3f84b372468f7768a7ca4775227afd105075670649474ba6524ea028175d5e0c",
    "zh:60a016a6d4bd6a8f96ffdef5f9bd37863a8124056c39dbaf282c9713ceac06e8",
    "zh:66e1fe61b78d7f35b5e1ed0d150dfa4997f32c877627c573b51735ab0c794d8e",
    "zh:6d4b832f2147dae47da68d80a7d7cd66cb799205ed6b476ae490b2e2c3087d49",
    "zh:bdf6555b6106ee5b597aa5e2ffed25d442f0e9ded1b531b0864c7d70d6b40c8b",
    "zh:c2095125ce9f9627091fc673a3ca673c66caa288e38970ae585869c89cd5946d",
    "zh:d43feedc9f6e0a49d208e4bac355ca0e843038c8f87cb8d3bb2355830d6e8dce",
    "zh:f569b65999264a9416862bca5cd2a6177d94ccb0424f3a4ef424428912b9cb3c",
    "zh:f80bf9c3bef00ba4738d46c7e6170d1eb7f49e20a081acffa33a39035df86326",
  ]
}

provider "registry.terraform.io/hashicorp/google-beta" {
  version = "4.63.1"
  hashes = [
    "h1:pqqFiQv23kiEbVk0OKRoT0+gxLZGsB28BUih+DZu/YM=",
    "zh:03677a3781a5b4a49c64fc2cbf46912c8b1c13b95a36297e799df1b720871c87",
    "zh:0a646edbb433bdda0dccc84af60b3e3460fe5d71341001ec8574cfeeef3948ac",
    "zh:2cce8e374d4a4ca046b1abbbe5fe50090f731cf69783b3333bb3594e7e7ff340",
    "zh:655a3e0805c125da33f60e0a0de5c0efaeab42a97e45a0c4bbcaaad1b38f6e09",
    "zh:6d7470e4bf1ffc9915371a3aec01b6fd187c267eddd34378fda9f8793d7ae49a",
    "zh:734a18e973a551b293e650806b77dfbca3c9a8c45aa087a1a34d6be5d4a5fe50",
    "zh:97a6512247144c9ebe47bb189a831293c815bff0eb91d9a8b5c3240041ee794a",
    "zh:a5f9a4290d0a0f6988c0139e64a9194ea96d711657669d5f52d18dd4738f2bce",
    "zh:ace0af5e78bc5a829eefddbe32c360a5989128f8c999e30036961f692055ea61",
    "zh:b01839915cd0da6522076e54656a1fe01eac72013f2567c3994b865714a973be",
    "zh:bd68231046fe56b1cec25a51c484df6327bb7856638cf5e16dd2e686764ddc87",
    "zh:f569b65999264a9416862bca5cd2a6177d94ccb0424f3a4ef424428912b9cb3c",
  ]
}

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
variables.tf

variables.tf
variable "gcp_svc_key" {}
variable "gcp_project" {}
variable "gcp_region" {}

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
terraform.tfvars

terraform.tfvars
gcp_svc_key = "..lateral-academy-314813-9ca87e8e0647.json"
gcp_project = "lateral-academy-314813
gcp_region = "us-east1"  

Prompt
-> github cd Desktop
Desktop ->cd Rodrigo
Desktop/Rodrigo->cd Visual Studio Code
Desktop/Rodrigo/Visual Studio Code->cd FreeCodeCamp
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp->cd Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
->cd freecodecamp-terraform-with-gcp
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform – Infrastructure as Code Course/freecodecamp-terraform-with-gcp ->cd infra
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform – Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terraform init 
Platform – Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terraform plan 
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the followed symbols:
create
Terraform will perform the following actions:
# google_storage_bucket.website will be created
+resource “google_storage_bucket” “website” {
force_destroy              = false
id                                 = (know after apply)
labels                           = (know after apply)
location                        = “US”
name                           = “example-website-by-rishab”
…
}
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform – Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terraform apply
google_storage_bucket.website: …
google_storage_bucket_object.static_site_src: …
google_storage_object_access_control.public_rule: …
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform –  Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->

Google Cloud UI 
https://cloud.google.com/ 
Cloud Storage
Buckets
Name                                       Created                              Location Type       Location       
example-website-by-rishab      30 May 2023, 16:39:38      Multi-Region         US
example-website-by-rishab
Objects
Name              Size      Type
index.html       2 KB      text/html, charset=utf-8
Objects details
Live Object
Overview
   Type 
   Size
   Created
   Last modified 
   Storage class
   Custom time
   Public URL                https://storage.googleapis.com/example-website-by-rishab/index.html 
   Authenticated URL
   …
Permission
   public access
…

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
main.tf

main.tf
# Bucket to store website
resource "google_storage_bucket" "website" {
  provider = google
  name     = "example-rishab-coffee7"
  location = "US"
}

# Make new objects public
resource "google_storage_object_access_control" "public_rule" {
  object = google_storage_bucket_object.static_site_src.output_name
  bucket = google_storage_bucket.website.name
  role   = "READER"
  entity = "allUsers"
}

# Upload the html file to the bucket
resource "google_storage_bucket_object" "static_site_src" {
  name   = "index.html"
  source = "../website/index.html"
  bucket = google_storage_bucket.website.name
  
}

# Reserve an external IP
resource "google_compute_global_address" "website" {
  provider = google
  name     = "website-lb-ip"
}

Google Cloud UI
Network services 
Cloud DNS
Zones
Zone Name        DNS Name            DNSSEC    Description      Zone Type
rishab-example   gcp.rishab.cloud    On              GCP ZONE     Public
Create Zone
Create a DNS zone
Zone Type
public
Zone name
terraform-gcp
DNS Name
test.rishab.cloud
Create
Zone details
terraform-gcp
Record sets
DNS name            Type
test.rishab.cloud    NS ( Name servers )
Resource recorded set details
DNS name           test.rishab.cloud
type                      NS
TTL(seconds)       21600
Routing data
Data
ns-cloud-b1.googledomains.com
ns-cloud-b2.googledomains.com
ns-cloud-b3.googledomains.com
ns-cloud-b4.googledomains.com

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
Infra
main.tf

main.tf
# Bucket to store website
resource "google_storage_bucket" "website" {
  provider = google
  name     = "example-rishab-coffee7"
  location = "US"
}

# Make new objects public
resource "google_storage_object_access_control" "public_rule" {
  object = google_storage_bucket_object.static_site_src.output_name
  bucket = google_storage_bucket.website.name
  role   = "READER"
  entity = "allUsers"
}

# Upload the html file to the bucket
resource "google_storage_bucket_object" "static_site_src" {
  name   = "index.html"
  source = "../website/index.html"
  bucket = google_storage_bucket.website.name
  
}

# Reserve an external IP
resource "google_compute_global_address" "website" {
  provider = google
  name     = "website-lb-ip"
}

# Get the managed DNS zone
data "google_dns_managed_zone" "gcp_coffeetime_dev" {
  provider = google
  name     = "rishab-example"
}

# Add the IP to the DNS
resource "google_dns_record_set" "website" {
  provider     = google
  name         = "website.${data.google_dns_managed_zone.gcp_coffeetime_dev.dns_name}"
  type         = "A"
  ttl          = 300
  managed_zone = data.google_dns_managed_zone.gcp_coffeetime_dev.name
  rrdatas      = [google_compute_global_address.website.address]
}

# Add the bucket as a CDN backend
resource "google_compute_backend_bucket" "website-backend" {
  provider    = google
  name        = "website-backend"
  description = "Contains files needed by the website"
  bucket_name = google_storage_bucket.website.name
  enable_cdn  = true
}
# GCP URL MAP
resource "google_compute_url_map" "website" {
  provider        = google
  name            = "website-url-map"
  default_service = google_compute_backend_bucket.website-backend.self_link
    host_rule {
    hosts        = ["*"]
    path_matcher = "allpaths"
  }

  path_matcher {
    name            = "allpaths"
    default_service = google_compute_backend_bucket.website-backend.self_link
  }
}

# GCP target proxy
resource "google_compute_target_https_proxy" "website" {
  provider         = google
  name             = "website-target-proxy"
  url_map          = google_compute_url_map.website.self_link
  ssl_certificates = [google_compute_managed_ssl_certificate.website.self_link]
}

# GCP forwarding rule
resource "google_compute_global_forwarding_rule" "default" {
  provider              = google
  name                  = "website-forwarding-rule"
  load_balancing_scheme = "EXTERNAL"
  ip_address            = google_compute_global_address.website.address
  ip_protocol           = "TCP"
  port_range            = "443"
  target                = google_compute_target_https_proxy.website.self_link
}

Prompt
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform –  Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terradorm plan
…
Plan: 5 to add, 0 to change, 0 to destroy.
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform –  Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terraform apply
…
Apply completed ! Resources: 5 to add, 0 to change, 0 to destroy. 

Google Cloud UI
Load Balancing ( Search Bar )
Name                   Load balancer type      Protocols   Regions   Backends
website-url-map   HTTP(S) (Classic)        HTTP                         1 backend bucket
Load balancer details
website-url-map
Details
Frontend 
Protocol      Ip Port                   Certificate     SSL Policy     Network Tier
HTTP          34.36.172.81:80                                                Premium
Host and Path Rules
Hosts                                 Paths                                   Backend
All unmatched ( default )    All unmatched ( default )     website-bucket
Backend
Backend buckets
1.website-bucket
Storage bucket name           Cloud CDN                             Edge Security Policy
example-website-by-rishab   enabled View CDN Details    none
http://34.36.172.81/index.html 
Google Cloud UI
Network services 
Cloud DNS
Zones
Zone Name        DNS Name            DNSSEC    Description      Zone Type
rishab-example   gcp.rishab.cloud    On              GCP ZONE     Public
Zone details 
rishab-example
Record sets                          Type     TTL (seconds)   Routing Policy
website.gcp.rishab.cloud       A          300                    Default 
Resource record set details
…
Routing data
Data
34.36.172.81
http://website.gcp.rishab.cloud/index.html 
Google Cloud
Security
Certificate Manager
website-cert
…
domain                                    Status
website.gcp.rishab.cloud         Provisioning 
…

Prompt
Desktop/Rodrigo/Visual Studio Code/FreeCodeCamp/ Learn Terraform with Google Cloud Platform –  Infrastructure as Code Course/freecodecamp-terraform-with-gcp/infra->terraform destroy

Visual Studio Code
Explorer 
OPEN EDITORS
Learn Terraform with Google Cloud Platform – Infrastructure as Code Course
.gitignore

.gitignore
# Local .terraform directories
**/.terraform/*

# .tfstate files
*.tfstate
*.tfstate.*

# Crash log files
crash.log
crash.*.log

# Exclude all .tfvars files, which are likely to contain sensitive data, such as
# password, private keys, and other secrets. These should not be part of version 
# control as they are data points which are potentially sensitive and subject 
# to change depending on the environment.
*.tfvars
*.tfvars.json

# Ignore override files as they are usually used to override resources locally and so
# are not checked in
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Include override files you do wish to add to version control using negated pattern
# !example_override.tf

# Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
# example: *tfplan*

# Ignore CLI configuration files
.terraformrc
terraform.rc

#Ignore GCP SVC Key
lateral-academy-svc-key-gcp.json




 
