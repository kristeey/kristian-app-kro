# Kristian App KRO Example

## Install KRO in your Kubernetes Cluster

1. **Fetch the latest KRO version:**
   ```sh
   export KRO_VERSION=$(curl -sL https://api.github.com/repos/kubernetes-sigs/kro/releases/latest | jq -r '.tag_name | ltrimstr("v")')
   echo $KRO_VERSION
   ```

2. **Install KRO using Helm:**
   ```sh
   helm install kro oci://registry.k8s.io/kro/charts/kro --namespace kro --create-namespace --version=${KRO_VERSION}
   ```

3. **Verify the installation:**
   ```sh
   helm -n kro list
   ```

   This will install the KRO operator in the `kro` namespace.

## Apply the ResourceGraphDefinition (RGD)

1. **Clone this repository and change to the directory:**
   ```sh
   git clone git@github.com:kristeey/kristian-app-kro.git
   cd kristian-app-kro
   ```

2. **Apply the RGD:**
   ```sh
   kubectl apply -f kristian-app-rgd.yaml
   ```

   This will create the ResourceGraphDefinition in your cluster.

## Create an Application Instance

1. **Edit or use the provided example:**
   - See `example/kristian-app.yaml` for a sample instance.

2. **Apply the instance:**
   ```sh
   kubectl apply -f example/kristian-app.yaml
   ```

   This will create a KristianApp instance based on your RGD.

## Useful Commands

- Check the status of your RGD:
  ```sh
  kubectl get rgd
  kubectl describe rgd kristian-app
  ```
- Check the status of your KristianApp instance:
  ```sh
  kubectl get kristianapp
  kubectl describe kristianapp <instance-name>
  ```

---

For more information, see the [KRO documentation](https://kro.run/docs/).
