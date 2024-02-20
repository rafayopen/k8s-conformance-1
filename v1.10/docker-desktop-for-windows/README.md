# Docker Desktop for Windows

## Reproduce conformance results

1. Download and  install Docker Desktop for Windows 18.05.0-win67 (Edge channel) : https://download.docker.com/win/edge/18263/Docker%20for%20Windows%20Installer.exe
2. In Docker Desktop settings, in the Kubernetes pane, enable Kubernetes to create a cluster on your local machine. 
3. Follow conformance test instructions from https://github.com/cncf/k8s-conformance/blob/master/instructions.md
: run `curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl apply -f -`, and get the results using `kubectl cp`
