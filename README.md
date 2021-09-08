# crc
## CodeReady Containers on Ubuntu

1. Use a non root user on Ubuntu OS to setup crc so use an existing non root user or create a new user something like 'crc'
2. Make sure your laptop or vm has 12 GB of memory. If you dont try adding virtual memory or swap on in case of linux.
3. Run following 2 commands to skip the RHEL specific checks.
```
crc config set skip-check-daemon-systemd-sockets true
crc config set skip-check-daemon-systemd-unit true
```
4. If you already attempted `crc setup` with failed attempt then first run following commands:
```
crc delete
crc cleanup 
rm -Rrf $HOME/.crc
```
5. Activate user network mode
```
crc config set network-mode user
```
6. Most importantly run the crc daemon else you will not be able to run crc. This should be run in a separate terminal window.
```
crc daemon
```
7. And you must get the following output
```
crc@rock1:~/OpenShift_CRC$ crc daemon
INFO Checking if running as non-root
INFO Checking if running inside WSL2
INFO Checking if crc-admin-helper executable is cached
INFO Checking for obsolete admin-helper executable
INFO Checking if running on a supported CPU architecture
INFO Checking minimum RAM requirements
INFO Checking if crc executable symlink exists
INFO Checking if Virtualization is enabled
INFO Checking if KVM is enabled
INFO Checking if libvirt is installed
INFO Checking if user is part of libvirt group
INFO Checking if active user/process is currently part of the libvirt group
INFO Checking if libvirt daemon is running
INFO Checking if a supported libvirt version is installed
INFO Checking if crc-driver-libvirt is installed
INFO Checking crc daemon systemd socket units
WARN Skipping above check...
INFO Checking if AppArmor is configured
INFO Checking if vsock is correctly configured
INFO listening vsock://:1024
INFO listening /home/crc/.crc/crc-http.sock

```
8. When you fire crc start command then you will be asked for Pull Secret which you would have copied from RedHat site.
```
crc@rock1:~$ crc start
INFO Checking if running as non-root
INFO Checking if running inside WSL2
INFO Checking if crc-admin-helper executable is cached
INFO Checking for obsolete admin-helper executable
INFO Checking if running on a supported CPU architecture
INFO Checking minimum RAM requirements
INFO Checking if crc executable symlink exists
INFO Checking if Virtualization is enabled
INFO Checking if KVM is enabled
INFO Checking if libvirt is installed
INFO Checking if user is part of libvirt group
INFO Checking if active user/process is currently part of the libvirt group
INFO Checking if libvirt daemon is running
INFO Checking if a supported libvirt version is installed
INFO Checking if crc-driver-libvirt is installed
INFO Checking crc daemon systemd socket units
WARN Skipping above check...
INFO Checking if AppArmor is configured
INFO Checking if vsock is correctly configured
CodeReady Containers requires a pull secret to download content from Red Hat.
You can copy it from the Pull Secret section of https://cloud.redhat.com/openshift/create/local.
? Please enter the pull secret
```
9. Screenshot from RedHat site to pull secret.
![image](https://user-images.githubusercontent.com/53788319/132544032-b32f4d02-18cf-40b6-a52a-7fdafcd7fb5b.png)

10. Once you enter (paste) the Pull Secret, this will mask your secret, and the output will be something similar to following:
```
? Please enter the pull secret ******************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
WARN Cannot add pull secret to keyring: failed to unlock correct collection '/org/freedesktop/secrets/aliases/default'
INFO Loading bundle: crc_libvirt_4.8.4...
INFO Creating CodeReady Containers VM for OpenShift 4.8.4...
INFO Generating new SSH Key pair...
INFO Generating new password for the kubeadmin user
INFO Starting CodeReady Containers VM for OpenShift 4.8.4...
INFO CodeReady Containers instance is running with IP 127.0.0.1

INFO CodeReady Containers VM is running
INFO Updating authorized keys...
INFO Check internal and public DNS query...
INFO Check DNS query from host...
WARN Wildcard DNS resolution for apps-crc.testing does not appear to be working
INFO Verifying validity of the kubelet certificates...
INFO Starting OpenShift kubelet service
INFO Waiting for kube-apiserver availability... [takes around 2min]
INFO Adding user's pull secret to the cluster...
INFO Updating SSH key to machine config resource...
INFO Waiting for user's pull secret part of instance disk...
INFO Changing the password for the kubeadmin user
INFO Updating cluster ID...
INFO Updating root CA cert to admin-kubeconfig-client-ca configmap...
INFO Starting OpenShift cluster... [waiting for the cluster to stabilize]
INFO 6 operators are progressing: dns, image-registry, kube-scheduler, network, openshift-controller-manager, ...
INFO 4 operators are progressing: image-registry, kube-scheduler, openshift-controller-manager, service-ca
INFO 5 operators are progressing: authentication, image-registry, kube-apiserver, kube-scheduler, service-ca
INFO 4 operators are progressing: authentication, image-registry, kube-apiserver, kube-scheduler
INFO 4 operators are progressing: authentication, kube-apiserver, kube-scheduler, openshift-controller-manager
INFO 3 operators are progressing: authentication, kube-apiserver, openshift-controller-manager
INFO 3 operators are progressing: authentication, kube-apiserver, openshift-controller-manager
INFO Operator kube-apiserver is progressing
INFO Operator kube-apiserver is progressing
INFO Operator kube-apiserver is progressing
INFO All operators are available. Ensuring stability...
INFO Operators are stable (2/3)...
INFO Operators are stable (3/3)...
INFO Adding crc-admin and crc-developer contexts to kubeconfig...
Started the OpenShift cluster.

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: s3MSo-oKMzC-4naxn-z3ncH

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443

```
11. This takes a while and you are done. Now you may run the commands printed as output like `eval $(crc oc-env)` and `oc login -u developer https://api.crc.testing:6443`
