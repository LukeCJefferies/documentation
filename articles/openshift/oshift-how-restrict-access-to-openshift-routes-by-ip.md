---
title: How to restrict access to a route in OpenShift by the source public IP address
description: Restrict access to OpenShift routes by the source public IP address
services: openshift
author: Mudasar Hussain
toc_rootlink: How To
toc_sub1: 
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Restrict access to OpenShift routes by the source public IP address
toc_fullpath: How To/restricting-access-to-openshift-routes-by-ip.md
toc_mdlink: oshift-how-restrict-access-to-openshift-routes-by-ip.md
---

# How to only allow trusted IP's to be able to access routes in Openshift

## Overview

This knowledge centre article explains how OpenShift developers can restrict access to the routes they create to their deployed services in OpenShift by IP address. This can be done to increase the security of a route by only allowing trusted IP's to access the OpenShift route.

### Intended audience

OpenShift developers who have already created and deployed services into OpenShift and also created routes for those services and exposed those routes. This article helps those users to further secure access to those exposed routes by restricting access to those exposed routes by only allowing trusted IP's to be able to access those routes.

## Restricting access to a route

After creating and exposing a route in OpenShift in the usual manner, you can then add an annotation to the route specifying the IP address(es) that you would like to whitelist.
  
> [!IMPORTANT]
> Whitelisting a IP address automaticly blacklists everything else.
  
  You apply the annotation to a route in the following manner:
  
    oc annotate route <route_name> haproxy.router.openshift.io/ip_whitelist=<ip_address>

> [!IMPORTANT]
> You must do this for every route that you wish to apply the whitelisting to.

## Examples

To allow a single IP address through to the route, use the following:
  
    oc annotate route myroute haproxy.router.openshift.io/ip_whitelist=192.168.1.10

To allow a several IP addresses through to the route, separate each IP with a space:

    oc annotate route myroute haproxy.router.openshift.io/ip_whitelist=192.168.1.10 192.168.1.11 192.168.1.12

To allow a network CIDR through to the route, decrlare the network CIDR as so:

    oc annotate route myroute haproxy.router.openshift.io/ip_whitelist=192.168.1.10/24

You can even use a mix of IP addresses and a network CIDR:

    oc annotate route myroute haproxy.router.openshift.io/ip_whitelist=192.168.1.10 180.5.61.153 192.168.1.0/24 10.0.0.0/8

## More information

For further infomation, see the following: [Openshift Documentation](https://docs.openshift.com/container-platform/3.9/architecture/networking/routes.html)


## Feedback

If you have any comments on this document or any other aspect of your UKCloud experience, send them to <products@ukcloud.com>.