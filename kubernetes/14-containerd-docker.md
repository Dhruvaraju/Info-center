
- Kubernetes dropped direct support for docker 
- Kubernetes supports any container environment that can adhere to Container runtime specifications.
- Kubernetes supports containerd
- With containerd a command line utility called as `ctr` is provided with limited support to connect with containers.
- `nerdctl` is a command line tool from community to interact with containerd, it is almost on par with docker cli.

- With kubernetes, container runtime a command line utility called as `crictl` is available
- `crictl` is a community driven tool, it is compatible with all CRI compatible runtimes.
s