### Cartographer supply chain that supports passing config parameters to Cloud Native Buildpacks

This has been tested with [Tanzu Application Platform](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/index.html) Beta 3.

This repo contains a [Cartographer](https://cartographer.sh/) supply chain that allows configuration parameters to be passed to [Cloud Native Buildpacks](https://buildpacks.io/). When using this supply chain, any workload parameter that begins with "BP_" will be included in the [kpack](https://github.com/pivotal/kpack) image YAML.

Create the supply chain:

* `kubectl create -f clusterimagetemplate.yaml`
* `kubectl create -f clustersupplychain.yaml`

Create a workload that uses the supply chain (requires the [tanzu CLI](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/0.3/tap-0-3/GUID-install-general.html#cli-and-plugin)):

* `tanzu apps workload create dotnet-accelerator --git-repo https://github.com/fjb4/tap-web-demo --git-branch main --type web-bp --param BP_DOTNET_PROJECT_PATH=src/Tanzu.WebDemo`

Note that using the supply chain requires you to specify a workload type of "web-bp". Any workload parameters that begin with "BP_" will be include in the kpack image YAML.

The example above shows how to pass the [BP_DOTNET_PROJECT_PATH](https://paketo.io/docs/howto/dotnet-core/#using-bp_dotnet_project_path) parameter to the .NET buildpack. This is necessary when building a .NET application where the project file is not in the root folder.

