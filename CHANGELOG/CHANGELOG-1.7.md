# Changelog 1.7

## 1.7.0 - 2022-06-15

### Added

- Add TrafficControl feature to control the transmission of Pod traffic; it allows users to mirror or redirect traffic originating from specific Pods or destined for specific Pods to a local network device or a remote destination via a tunnel of various types. ([#3644](https://github.com/antrea-io/antrea/pull/3644) [#3580](https://github.com/antrea-io/antrea/pull/3580) [#3487](https://github.com/antrea-io/antrea/pull/3487), [@tnqn] [@hongliangl] [@wenqiq])
  * Refer to [this document](https://github.com/antrea-io/antrea/blob/release-1.7/docs/traffic-control.md) for more information about this feature.
  * Refer to [this cookbook](https://github.com/antrea-io/antrea/blob/release-1.7/docs/cookbooks/ids/README.md) for more information about using this feature to provide network-based intrusion detection service to your Pods.
- Add support for the IPsec Certificate-based Authentication. ([#3778](https://github.com/antrea-io/antrea/pull/3778), [@xliuxu])
  * Add an Antrea Agent configuration option `ipsec.authenticationMode` to specify authentication mode. Supported options are "psk" (default) and "cert".
  * Add an Antrea Controller configuration option `ipsecCSRSigner.autoApprove` to specify the auto-approve policy of Antrea CSR signer for IPsec certificates management. By default, Antrea will auto-approve the CertificateSingingRequest (CSR) if it is verified.
  * Add an Antrea Controller configuration option `ipsecCSRSigner.selfSignedCA` to specify whether to use auto-generated self-signed CA certificate. By default, Antrea will auto-generate a self-signed CA certificate.
- Add the following capabilities to Antrea-native policies:
  * Add support for matching ICMP traffic. ([#3472](https://github.com/antrea-io/antrea/pull/3472), [@GraysonWu])
  * Add support for matching multicast and IGMP traffic. ([#3660](https://github.com/antrea-io/antrea/pull/3660), [@liu4480])
  * Add support for rule-level statistics for multicast and IGMP traffic. ([#3449](https://github.com/antrea-io/antrea/pull/3449), [@ceclinux])
- Add the following capabilities to the Multicast feature:
  * Add `antctl get podmulticaststats` command to query Pod-level multicast traffic statistics in Agent mode. ([#3449](https://github.com/antrea-io/antrea/pull/3449), [@ceclinux])
  * Add "MulticastGroup" API to query Pods that have joined multicast groups; `kubectl get multicastgroups` can generate requests and output responses of the API. ([#3354](https://github.com/antrea-io/antrea/pull/3354) [#3449](https://github.com/antrea-io/antrea/pull/3449), [@ceclinux])
  * Add an Antrea Agent configuration option `multicast.igmpQueryInterval` to specify the interval at which the antrea-agent sends IGMP queries to Pods. ([#3819](https://github.com/antrea-io/antrea/pull/3819), [@liu4480])
- Add the following capabilities to the Multi-cluster feature:
  * Add the Multi-cluster Gateway functionality which supports routing Multi-cluster Service traffic across clusters through tunnels between the Gateway Nodes. It enables Multi-cluster Service access across clusters, without requiring direct reachability of Pod IPs between clusters. ([#3689](https://github.com/antrea-io/antrea/pull/3689) [#3463](https://github.com/antrea-io/antrea/pull/3463) [#3603](https://github.com/antrea-io/antrea/pull/3603), [@luolanzone])
  * Add a number of `antctl mc` subcommands for bootstrapping Multi-cluster; refer to the [Multi-cluster antct document](https://github.com/antrea-io/antrea/blob/release-1.7/docs/multicluster/antctl.md) for more information. ([#3474](https://github.com/antrea-io/antrea/pull/3474), [@hjiajing])
- Add the following capabilities to secondary network IPAM:
  * Add support for IPAM for Pod secondary networks managed by Multus. ([#3529](https://github.com/antrea-io/antrea/pull/3529), [@jianjuns])
  * Add support for multiple IPPools. ([#3606](https://github.com/antrea-io/antrea/pull/3606), [@jianjuns])
  * Add support for static addresses. ([#3633](https://github.com/antrea-io/antrea/pull/3633), [@jianjuns])
- Add support for NodePortLocal on Windows. ([#3453](https://github.com/antrea-io/antrea/pull/3453), [@XinShuYang])
- Add support for Traceflow on Windows. ([#3022](https://github.com/antrea-io/antrea/pull/3022), [@gran-vmv])
- Add support for containerd to antrea-eks-node-init.yml. ([#3840](https://github.com/antrea-io/antrea/pull/3840), [@antoninbas])
- Add an Antrea Agent configuration option `disableTXChecksumOffload` to support cases in which the datapath's TX checksum offloading does not work properly. ([#3832](https://github.com/antrea-io/antrea/pull/3832), [@tnqn])
- Add support for InternalTrafficPolicy in AntreaProxy. ([#2792](https://github.com/antrea-io/antrea/pull/2792), [@hongliangl])
- Add the following documentations:
  * Add [documentation](https://github.com/antrea-io/antrea/blob/release-1.7/docs/security.md#protecting-your-cluster-against-privilege-escalations) for the Antrea Agent RBAC permissions and how to restrict them using Gatekeeper/OPA. ([#3694](https://github.com/antrea-io/antrea/pull/3694), [@antoninbas])
  * Add [quick start guide](https://github.com/antrea-io/antrea/blob/release-1.7/docs/multicluster/quick-start.md) for Antrea Multi-cluster. ([#3853](https://github.com/antrea-io/antrea/pull/3853), [@luolanzone] [@jianjuns])
  * Add [documentation](https://github.com/antrea-io/antrea/blob/release-1.7/docs/antrea-proxy.md) for the AntreaProxy feature. ([#3679](https://github.com/antrea-io/antrea/pull/3679), [@antoninbas])
  * Add [documentation](https://github.com/antrea-io/antrea/blob/release-1.7/docs/antrea-ipam.md#ipam-for-secondary-network) for secondary network IPAM. ([#3634](https://github.com/antrea-io/antrea/pull/3634), [@jianjuns])

### Changed

- Optimize generic traffic performance by reducing OVS packet recirculation. ([#3858](https://github.com/antrea-io/antrea/pull/3858), [@tnqn])
- Optimize NodePort traffic performance by reducing OVS packet recirculation. ([#3862](https://github.com/antrea-io/antrea/pull/3862), [@hongliangl])
- Improve validation for IPPool CRD. ([#3570](https://github.com/antrea-io/antrea/pull/3570), [@jianjuns])
- Improve validation for `egress.to.namespaces.match` of AntreaClusterNetworkPolicy rules. ([#3727](https://github.com/antrea-io/antrea/pull/3727), [@qiyueyao])
- Deprecate the Antrea Agent configuration option `multicastInterfaces` in favor of `multicast.multicastInterfaces`. ([#3898](https://github.com/antrea-io/antrea/pull/3898), [@tnqn])
- Reduce permissions of Antrea Agent ServiceAccount. ([#3691](https://github.com/antrea-io/antrea/pull/3691), [@xliuxu])
- Create a Secret in the Antrea manifest for the antctl and antrea-agent ServiceAccount as K8s v1.24 no longer creates a token for each ServiceAccount automatically. ([#3730](https://github.com/antrea-io/antrea/pull/3730), [@antoninbas])
- Implement garbage collector for IP Pools to clean up allocations and reservations for which owner no longer exists. ([#3672](https://github.com/antrea-io/antrea/pull/3672), [@annakhm])
- Preserve client IP if the selected Endpoint is local regardless of ExternalTrafficPolicy. ([#3604](https://github.com/antrea-io/antrea/pull/3604), [@hongliangl])
- Add a Helm chart for Antrea and use the Helm templates to generate the standard Antrea YAML manifests. ([#3578](https://github.com/antrea-io/antrea/pull/3578), [@antoninbas])
- Make "Agent mode" antctl work out-of-the-box on Windows. ([#3645](https://github.com/antrea-io/antrea/pull/3645), [@antoninbas])
- Truncate SessionAffinity timeout values of Services instead of wrapping around. ([#3609](https://github.com/antrea-io/antrea/pull/3609), [@antoninbas])
- Move Antrea Windows log dir from `C:\k\antrea\logs\` to `C:\var\log\antrea\`. ([#3416](https://github.com/antrea-io/antrea/pull/3416), [@GraysonWu])
- Limit max number of data values displayed on Grafana panels. ([#3812](https://github.com/antrea-io/antrea/pull/3812), [@heanlan])
- Support deploying ClickHouse with Persistent Volume. ([#3608](https://github.com/antrea-io/antrea/pull/3608), [@yanjunz97])
- Remove support for ELK Flow Collector. ([#3738](https://github.com/antrea-io/antrea/pull/3738), [@heanlan])
- Improve documentation for Antrea-native policies. ([#3512](https://github.com/antrea-io/antrea/pull/3512), [@Dyanngg])
- Update OVS version to 2.17.0. ([#3591](https://github.com/antrea-io/antrea/pull/3591), [@antoninbas])

### Fixed

- Fix Egress not working with kube-proxy IPVS strictARP mode. ([#3837](https://github.com/antrea-io/antrea/pull/3837), [@xliuxu])
- Fix intra-Node Pod traffic bypassing Ingress NetworkPolicies in some scenarios. ([#3809](https://github.com/antrea-io/antrea/pull/3809), [@hongliangl])
- Fix FQDN policy support for IPv6. ([#3869](https://github.com/antrea-io/antrea/pull/3869), [@tnqn])
- Fix multicast not working if the AntreaPolicy feature is disabled. ([#3807](https://github.com/antrea-io/antrea/pull/3807), [@liu4480])
- Fix tolerations for Pods running on control-plane for Kubernetes >= 1.24. ([#3731](https://github.com/antrea-io/antrea/pull/3731), [@xliuxu])
- Fix DNS resolution error of antrea-agent on AKS by using `ClusterFirst` dnsPolicy. ([#3701](https://github.com/antrea-io/antrea/pull/3701), [@tnqn])
- Clean up stale routes installed by AntreaProxy when ProxyAll is disabled. ([#3465](https://github.com/antrea-io/antrea/pull/3465), [@hongliangl])
- Ensure that Service traffic does not bypass NetworkPolicies when ProxyAll is enabled on Windows. ([#3510](https://github.com/antrea-io/antrea/pull/3510), [@hongliangl])
- Use IP and MAC to find virtual management adapter to fix Agent crash in some scenarios on Windows. ([#3641](https://github.com/antrea-io/antrea/pull/3641), [@wenyingd])
- Fix handling of the "reject" packets generated by the Antrea Agent to avoid infinite looping. ([#3569](https://github.com/antrea-io/antrea/pull/3569), [@GraysonWu])
- Fix export/import of Services with named ports when using the Antrea Multi-cluster feature. ([#3561](https://github.com/antrea-io/antrea/pull/3561), [@luolanzone])
- Fix Multi-cluster importer not working after leader controller restarts. ([#3596](https://github.com/antrea-io/antrea/pull/3596), [@luolanzone])
- Fix Endpoint ResourceExports not cleaned up after corresponding Service is deleted. ([#3652](https://github.com/antrea-io/antrea/pull/3652), [@luolanzone])  
- Fix pool CRD format in egress.md and service-loadbalancer.md. ([#3885](https://github.com/antrea-io/antrea/pull/3885), [@jianjuns])
- Fix infinite looping when Agent tries to delete a non-existing route. ([#3827](https://github.com/antrea-io/antrea/pull/3827), [@hongliangl])
- Fix race condition in ConntrackConnectionStore and FlowExporter. ([#3655](https://github.com/antrea-io/antrea/pull/3655), [@heanlan])

[@Atish-iaf]: https://github.com/Atish-iaf
[@Dyanngg]: https://github.com/Dyanngg
[@GraysonWu]: https://github.com/GraysonWu
[@XinShuYang]: https://github.com/XinShuYang
[@annakhm]: https://github.com/annakhm
[@antoninbas]: https://github.com/antoninbas
[@antrea-bot]: https://github.com/antrea-bot
[@ceclinux]: https://github.com/ceclinux
[@dependabot]: https://github.com/dependabot
[@dreamtalen]: https://github.com/dreamtalen
[@github-actions]: https://github.com/github-actions
[@gran-vmv]: https://github.com/gran-vmv
[@heanlan]: https://github.com/heanlan
[@hjiajing]: https://github.com/hjiajing
[@hongliangl]: https://github.com/hongliangl
[@jainpulkit22]: https://github.com/jainpulkit22
[@jianjuns]: https://github.com/jianjuns
[@leonstack]: https://github.com/leonstack
[@liu4480]: https://github.com/liu4480
[@luolanzone]: https://github.com/luolanzone
[@mohitsaxenaknoldus]: https://github.com/mohitsaxenaknoldus
[@qiyueyao]: https://github.com/qiyueyao
[@tnqn]: https://github.com/tnqn
[@vrabbi]: https://github.com/vrabbi
[@wenqiq]: https://github.com/wenqiq
[@wenyingd]: https://github.com/wenyingd
[@wsquan171]: https://github.com/wsquan171
[@xliuxu]: https://github.com/xliuxu
[@yanjunz97]: https://github.com/yanjunz97
[@yuntanghsu]: https://github.com/yuntanghsu
