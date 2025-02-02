A simple preprocessor for terraform.
====================================

```sh
USAGE:

  invade <template dir> <modules dir>
```

This script will copy all tf files in the template dir to the modules dir
and replace the `//invade <invader name> <args>` with the content of the
invader file located at `./invader/<invader name>.tf`.
The invader file is a piece of tf file with ERB template.
The args are formed as `key=value` pairs.

* version: 0.1.0 first release
* version: 0.2.0 support shell script
  You can use `#invade` for shell script.

Here's an example terraform resource that is invaded :)

```tf
resource "google_compute_instance" "leader" {
  name = "leader"
  machine_type = var.server_machine_type
  zone = var.zone
  tags = ["http-server", "https-server", "lb-health-check"]
  //invade server name=leader
}
//invade k3s_setup name=leader
//invade setup name=leader
```

The invader dir should go like this:

```
./invader/
├── k3s_setup.tf
├── server.tf
└── setup.tf
```

INSTALL
-------

Just copy the `invade` file to your `$PATH` dir.
