## policy.json
配置策略。每次进行API调用时，会采取对应的检查，policy.json文件发生更新后会立即生效。

目前支持的策略有三种：rule、role或者generic。

其中rule后面会跟一个文件名，例如
```
"get_floatingip": "rule:admin_or_owner",
```

其策略为rule:admin_or_owner，表明要从文件中读取具体策略内容。
role策略后面会跟一个role名称，表明只有指定role才可以执行。
generic策略则根据参数来进行比较。

```
{
    "context_is_admin":  "role:admin",
    "admin_or_owner": "rule:context_is_admin or tenant_id:%(tenant_id)s",
    "context_is_advsvc":  "role:advsvc",
    "admin_or_network_owner": "rule:context_is_admin or tenant_id:%(network:tenant_id)s",
    "admin_only": "rule:context_is_admin",
    "regular_user": "",
    "shared": "field:networks:shared=True",
    "shared_firewalls": "field:firewalls:shared=True",
    "external": "field:networks:router:external=True",
    "default": "rule:admin_or_owner",

    "create_subnet": "rule:admin_or_network_owner",
    "get_subnet": "rule:admin_or_owner or rule:shared",
    "update_subnet": "rule:admin_or_network_owner",
    "delete_subnet": "rule:admin_or_network_owner",

    "create_network": "",
    "get_network": "rule:admin_or_owner or rule:shared or rule:external or rule:context_is_advsvc",
    "get_network:router:external": "rule:regular_user",
    "get_network:segments": "rule:admin_only",
    "get_network:provider:network_type": "rule:admin_only",
    "get_network:provider:physical_network": "rule:admin_only",
    "get_network:provider:segmentation_id": "rule:admin_only",
    "get_network:queue_id": "rule:admin_only",
    "create_network:shared": "rule:admin_only",
    "create_network:router:external": "rule:admin_only",
    "create_network:segments": "rule:admin_only",
    "create_network:provider:network_type": "rule:admin_only",
    "create_network:provider:physical_network": "rule:admin_only",
    "create_network:provider:segmentation_id": "rule:admin_only",
    "update_network": "rule:admin_or_owner",
    "update_network:segments": "rule:admin_only",
    "update_network:shared": "rule:admin_only",
    "update_network:provider:network_type": "rule:admin_only",
    "update_network:provider:physical_network": "rule:admin_only",
    "update_network:provider:segmentation_id": "rule:admin_only",
    "update_network:router:external": "rule:admin_only",
    "delete_network": "rule:admin_or_owner",

    "create_port": "",
    "create_port:mac_address": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "create_port:fixed_ips": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "create_port:port_security_enabled": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "create_port:binding:host_id": "rule:admin_only",
    "create_port:binding:profile": "rule:admin_only",
    "create_port:mac_learning_enabled": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "get_port": "rule:admin_or_owner or rule:context_is_advsvc",
    "get_port:queue_id": "rule:admin_only",
    "get_port:binding:vif_type": "rule:admin_only",
    "get_port:binding:vif_details": "rule:admin_only",
    "get_port:binding:host_id": "rule:admin_only",
    "get_port:binding:profile": "rule:admin_only",
    "update_port": "rule:admin_or_owner or rule:context_is_advsvc",
    "update_port:fixed_ips": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "update_port:port_security_enabled": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "update_port:binding:host_id": "rule:admin_only",
    "update_port:binding:profile": "rule:admin_only",
    "update_port:mac_learning_enabled": "rule:admin_or_network_owner or rule:context_is_advsvc",
    "delete_port": "rule:admin_or_owner or rule:context_is_advsvc",

    "get_router:ha": "rule:admin_only",
    "create_router": "rule:regular_user",
    "create_router:external_gateway_info:enable_snat": "rule:admin_only",
    "create_router:distributed": "rule:admin_only",
    "create_router:ha": "rule:admin_only",
    "get_router": "rule:admin_or_owner",
    "get_router:distributed": "rule:admin_only",
    "update_router:external_gateway_info:enable_snat": "rule:admin_only",
    "update_router:distributed": "rule:admin_only",
    "update_router:ha": "rule:admin_only",
    "delete_router": "rule:admin_or_owner",

    "add_router_interface": "rule:admin_or_owner",
    "remove_router_interface": "rule:admin_or_owner",

    "create_firewall": "",
    "get_firewall": "rule:admin_or_owner",
    "create_firewall:shared": "rule:admin_only",
    "get_firewall:shared": "rule:admin_only",
    "update_firewall": "rule:admin_or_owner",
    "update_firewall:shared": "rule:admin_only",
    "delete_firewall": "rule:admin_or_owner",

    "create_firewall_policy": "",
    "get_firewall_policy": "rule:admin_or_owner or rule:shared_firewalls",
    "create_firewall_policy:shared": "rule:admin_or_owner",
    "update_firewall_policy": "rule:admin_or_owner",
    "delete_firewall_policy": "rule:admin_or_owner",

    "create_firewall_rule": "",
    "get_firewall_rule": "rule:admin_or_owner or rule:shared_firewalls",
    "update_firewall_rule": "rule:admin_or_owner",
    "delete_firewall_rule": "rule:admin_or_owner",

    "create_qos_queue": "rule:admin_only",
    "get_qos_queue": "rule:admin_only",

    "update_agent": "rule:admin_only",
    "delete_agent": "rule:admin_only",
    "get_agent": "rule:admin_only",

    "create_dhcp-network": "rule:admin_only",
    "delete_dhcp-network": "rule:admin_only",
    "get_dhcp-networks": "rule:admin_only",
    "create_l3-router": "rule:admin_only",
    "delete_l3-router": "rule:admin_only",
    "get_l3-routers": "rule:admin_only",
    "get_dhcp-agents": "rule:admin_only",
    "get_l3-agents": "rule:admin_only",
    "get_loadbalancer-agent": "rule:admin_only",
    "get_loadbalancer-pools": "rule:admin_only",

    "create_floatingip": "rule:regular_user",
    "update_floatingip": "rule:admin_or_owner",
    "delete_floatingip": "rule:admin_or_owner",
    "get_floatingip": "rule:admin_or_owner",

    "create_network_profile": "rule:admin_only",
    "update_network_profile": "rule:admin_only",
    "delete_network_profile": "rule:admin_only",
    "get_network_profiles": "",
    "get_network_profile": "",
    "update_policy_profiles": "rule:admin_only",
    "get_policy_profiles": "",
    "get_policy_profile": "",

    "create_metering_label": "rule:admin_only",
    "delete_metering_label": "rule:admin_only",
    "get_metering_label": "rule:admin_only",

    "create_metering_label_rule": "rule:admin_only",
    "delete_metering_label_rule": "rule:admin_only",
    "get_metering_label_rule": "rule:admin_only",

    "get_service_provider": "rule:regular_user",
    "get_lsn": "rule:admin_only",
    "create_lsn": "rule:admin_only"
}
```