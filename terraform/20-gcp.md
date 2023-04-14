- For terraform to work install gcloud sdk
- Then authorize it to login after completion
- To use terraform scripts run `gcloud auth application-default login`

https://www.fairwinds.com/blog/how-to-use-terraform-with-gke-a-step-by-step-guide-to-deploying-your-first-cluster

```
gcloud container clusters get-credentials gke-example --region us-central1
Fetching cluster endpoint and auth data.
kubeconfig entry generated for gke-example.
```

```
https://fig.io/manual/gcloud/container/clusters/get-credentials
```

https://cloud.google.com/sdk/gcloud/reference/container/clusters/get-credentials


example -vm instance

```hcl
# This code is compatible with Terraform 4.25.0 and versions that are backwards compatible to 4.25.0.
# For information about validating this Terraform code, see https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#format-and-validate-the-configuration

resource "google_compute_instance" "server-01" {
  boot_disk {
    auto_delete = true
    device_name = "server-01"

    initialize_params {
      image = "projects/debian-cloud/global/images/debian-10-buster-v20230306"
      size  = 10
      type  = "pd-balanced"
    }

    mode = "READ_WRITE"
  }

  can_ip_forward      = false
  deletion_protection = false
  enable_display      = false

  labels = {
    ec-src = "vm_add-tf"
    env    = "test"
  }

  machine_type = "e2-micro"
  name         = "server-01"

  network_interface {
    access_config {
      network_tier = "PREMIUM"
    }

    subnetwork = "projects/{project-name}/regions/asia-south1/subnetworks/default"
  }

  scheduling {
    automatic_restart   = true
    on_host_maintenance = "MIGRATE"
    preemptible         = false
    provisioning_model  = "STANDARD"
  }

  service_account {
    email  = ""
    scopes = ["https://www.googleapis.com/auth/devstorage.read_only", "https://www.googleapis.com/auth/logging.write", "https://www.googleapis.com/auth/monitoring.write", "https://www.googleapis.com/auth/service.management.readonly", "https://www.googleapis.com/auth/servicecontrol", "https://www.googleapis.com/auth/trace.append"]
  }

  shielded_instance_config {
    enable_integrity_monitoring = true
    enable_secure_boot          = false
    enable_vtpm                 = true
  }

  tags = ["http-server"]
  zone = "asia-south1-c"
}

```