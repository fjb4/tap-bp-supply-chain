## [Tanzu Application Platform](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/index.html) - Custom .NET [Supply Chain](https://cartographer.sh/)

These instructions describe how to add a custom supply chain to TAP, one that allows .NET applications to specify a custom project path.

Create the supply chain:

* `kubectl create -f clusterimagetemplate.yaml`
* `kubectl create -f clustersupplychain.yaml`

Create a workload that uses the supply chain (requires the [tanzu CLI](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/0.3/tap-0-3/GUID-install-general.html#cli-and-plugin)):

* `tanzu apps workload create dotnet-accelerator --git-repo https://github.com/fjb4/tap-web-demo --git-branch main --type web-dotnet --param project-path=src/Tanzu.WebDemo`

Note that using the supply chain requires you to specify a workload type of "web-dotnet". The project path can be given using the "project-path" parameter.

This has been tested with TAP beta 3.
