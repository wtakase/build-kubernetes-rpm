Build Kubernetes RPM for supporting Pod domain DNS search
====

Way to build
----
```bash
$ uname -r
3.10.0-229.el7.x86_64
$ cat /etc/redhat-release 
CentOS Linux release 7.1.1503 (Core)
$ curl -O ftp://rpmfind.net/linux/fedora/linux/development/rawhide/source/SRPMS/k/kubernetes-1.2.0-0.2.alpha1.git4c8e6f4.fc24.src.rpm
$ rpm -ih kubernetes-1.2.0-0.2.alpha1.git4c8e6f4.fc24.src.rpm 
$ sed -i -e "s/^Release:.*/Release:        wtakase0.2.alpha1.git%{k8s_shortcommit}%{?dist}/" -e "/^Patch12:.*/a Patch100:       add_pod_domain.patch" -e "/^\%patch12 -p1/a %patch100 -p1" ~/rpmbuild/SPECS/kubernetes.spec
$ cp add_pod_domain.patch ~/rpmbuild/SOURCES/
$ rpmbuild -bb rpmbuild/SPECS/kubernetes.spec
```
