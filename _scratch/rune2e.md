```sh
cd e2e
poetry install --no-root
```

If hangs, delete virtual env (`rm -rf ~/.cache/pypoetry/virtualenvs`) and retry

```sh
# Build the container locally
$ cd .. && PREFIX=ghcr.io/project-akri/akri LABEL_PREFIX=pr LOAD=1 make
# Save it as a tarbal
$ docker save ghcr.io/project-akri/akri/udev-discovery:pr > udev-discovery.tar
```

Install K3s
```sh
    curl -sfL https://get.k3s.io | sh -
    sudo addgroup k3s-admin
 sudo adduser $USER k3s-admin
 sudo usermod -a -G k3s-admin $USER
 sudo chgrp k3s-admin /etc/rancher/k3s/k3s.yaml
 sudo chmod g+r /etc/rancher/k3s/k3s.yaml
 su - $USER
   kubectl get no
```

Import udev discovery handler image into cluster
```sh
sudo k3s ctr image import udev-discovery.tar
```
# Start k3s cluster
# Load images into k3s containerd
# Run specifying to pull from local
$ poetry run pytest -v --distribution k3s  --test-version $(cat ../version.txt) --use-local
```

Output 
```
platform linux -- Python 3.10.12, pytest-7.3.1, pluggy-1.0.0 -- /home/kagold/.cache/pypoetry/virtualenvs/akri-e2e-8ptrDnqa-py3.10/bin/python
cachedir: .pytest_cache
rootdir: /home/kagold/projects/udev-discovery-handler/e2e
plugins: Faker-18.10.1
collected 2 items 

test_udev.py::test_dev_null_config PASSED                                                                [ 50%]
test_udev.py::test_grouped_config PASSED                                                                 [100%]
```