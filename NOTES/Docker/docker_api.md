docker-py 手册

[TOC]

Help on Client in module docker.client object:

class Client(requests.sessions.Session, docker.api.build.BuildApiMixin, docker.api.container.ContainerApiMixin, docker.api.daemon.DaemonApiMixin, docker.api.exec_api.ExecApiMixin, docker.api.image.ImageApiMixin, docker.api.network.NetworkApiMixin, docker.api.service.ServiceApiMixin, docker.api.swarm.SwarmApiMixin, docker.api.volume.VolumeApiMixin)
 |  Method resolution order:
 |      Client
 |      requests.sessions.Session
 |      requests.sessions.SessionRedirectMixin
 |      docker.api.build.BuildApiMixin
 |      docker.api.container.ContainerApiMixin
 |      docker.api.daemon.DaemonApiMixin
 |      docker.api.exec_api.ExecApiMixin
 |      docker.api.image.ImageApiMixin
 |      docker.api.network.NetworkApiMixin
 |      docker.api.service.ServiceApiMixin
 |      docker.api.swarm.SwarmApiMixin
 |      docker.api.volume.VolumeApiMixin
 |      __builtin__.object
 |  

## Methods defined here:

 |  
 ```__init__(self, base_url=None, version=None, timeout=60, tls=False, user_agent='docker-py/1.10.6', num_pools=25)```
 |  
 |  ```get_adapter(self, url)```
 |  
 |  ----------------------------------------------------------------------
 |  Class methods defined here:
 |  
 |  ```from_env(cls, **kwargs)``` from __builtin__.type
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors defined here:
 |  
 |  api_version
 |  
 |  ----------------------------------------------------------------------

####  Methods inherited from requests.sessions.Session:

 |  
 |  ```__enter__(self)```
 |  
 |  ```__exit__(self, *args)``
 |  
 |```  __getstate__(self)```
 |  
 | ``` __setstate__(self, state)```
 |  
 |  ```close(self)```
 |      Closes all adapters and as such the session
 |  
 | ``` delete(self, url, **kwargs)```
 |      Sends a DELETE request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 | ``` get(self, url, **kwargs)```
 |      Sends a GET request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 |```  head(self, url, **kwargs)```
 |      Sends a HEAD request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 | ``` merge_environment_settings(self, url, proxies, stream, verify, cert)```
 |      Check the environment and merge it with some settings.
 |      
 |      :rtype: dict
 |  
 | ``` mount(self, prefix, adapter)```
 |      Registers a connection adapter to a prefix.
 |      
 |      Adapters are sorted in descending order by prefix length.
 |  
 |  ```options(self, url, **kwargs)```
 |      Sends a OPTIONS request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 | ``` patch(self, url, data=None, **kwargs)```
 |      Sends a PATCH request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param data: (optional) Dictionary, bytes, or file-like object to send in the body of the :class:`Request`.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 | ``` post(self, url, data=None, json=None, **kwargs)```
 |      Sends a POST request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param data: (optional) Dictionary, bytes, or file-like object to send in the body of the :class:`Request`.
 |      :param json: (optional) json to send in the body of the :class:`Request`.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 | ``` prepare_request(self, request)```
 |      Constructs a :class:`PreparedRequest <PreparedRequest>` for
 |      transmission and returns it. The :class:`PreparedRequest` has settings
 |      merged from the :class:`Request <Request>` instance and those of the
 |      :class:`Session`.
 |      
 |      :param request: :class:`Request` instance to prepare with this
 |          session's settings.
 |      :rtype: requests.PreparedRequest
 |  
 |```  put(self, url, data=None, **kwargs)```
 |      Sends a PUT request. Returns :class:`Response` object.
 |      
 |      :param url: URL for the new :class:`Request` object.
 |      :param data: (optional) Dictionary, bytes, or file-like object to send in the body of the :class:`Request`.
 |      :param \*\*kwargs: Optional arguments that ``request`` takes.
 |      :rtype: requests.Response
 |  
 |  ```request(self, method, url, params=None, data=None, headers=None, cookies=None, files=None,auth=None, timeout=None, allow_redirects=True, proxies=None, hooks=None, stream=None, verify=None, cert=None, json=None)```
 |      Constructs a :class:`Request <Request>`, prepares it and sends it.
 |      Returns :class:`Response <Response>` object.
 |      
 |      :param method: method for the new :class:`Request` object.
 |      :param url: URL for the new :class:`Request` object.
 |      :param params: (optional) Dictionary or bytes to be sent in the query
 |          string for the :class:`Request`.
 |      :param data: (optional) Dictionary, bytes, or file-like object to send
 |          in the body of the :class:`Request`.
 |      :param json: (optional) json to send in the body of the
 |          :class:`Request`.
 |      :param headers: (optional) Dictionary of HTTP Headers to send with the
 |          :class:`Request`.
 |      :param cookies: (optional) Dict or CookieJar object to send with the
 |          :class:`Request`.
 |      :param files: (optional) Dictionary of ``'filename': file-like-objects``
 |          for multipart encoding upload.
 |      :param auth: (optional) Auth tuple or callable to enable
 |          Basic/Digest/Custom HTTP Auth.
 |      :param timeout: (optional) How long to wait for the server to send
 |          data before giving up, as a float, or a :ref:`(connect timeout,
 |          read timeout) <timeouts>` tuple.
 |      :type timeout: float or tuple
 |      :param allow_redirects: (optional) Set to True by default.
 |      :type allow_redirects: bool
 |      :param proxies: (optional) Dictionary mapping protocol or protocol and
 |          hostname to the URL of the proxy.
 |      :param stream: (optional) whether to immediately download the response
 |          content. Defaults to ``False``.
 |      :param verify: (optional) Either a boolean, in which case it controls whether we verify
 |          the server's TLS certificate, or a string, in which case it must be a path
 |          to a CA bundle to use. Defaults to ``True``.
 |      :param cert: (optional) if String, path to ssl client cert file (.pem).
 |          If Tuple, ('cert', 'key') pair.
 |      :rtype: requests.Response
 |  
 | ``` send(self, request, **kwargs)```
 |      Send a given PreparedRequest.
 |      
 |      :rtype: requests.Response
 |  
 |  ----------------------------------------------------------------------
 |  Data and other attributes inherited from requests.sessions.Session:
 |  
 | ``` __attrs__ = ['headers', 'cookies', 'auth', 'proxies', 'hooks', 'params...```
 |  
 |  ----------------------------------------------------------------------

####   Methods inherited from requests.sessions.SessionRedirectMixin:

 |  
 | ``` get_redirect_target(self, resp)```
 |      Receives a Response. Returns a redirect URI or ``None``
 |  
 |  ```rebuild_auth(self, prepared_request, response)```
 |      When being redirected we may want to strip authentication from the
 |      request to avoid leaking credentials. This method intelligently removes
 |      and reapplies authentication where possible to avoid credential loss.
 |  
 |  ```rebuild_method(self, prepared_request, response)```
 |      When being redirected we may want to change the method of the request
 |      based on certain specs or browser behavior.
 |  
 | ``` rebuild_proxies(self, prepared_request, proxies)```
 |      This method re-evaluates the proxy configuration by considering the
 |      environment variables. If we are redirected to a URL covered by
 |      NO_PROXY, we strip the proxy configuration. Otherwise, we set missing
 |      proxy keys for this URL (in case they were stripped by a previous
 |      redirect).
 |      
 |      This method also replaces the Proxy-Authorization header where
 |      necessary.
 |      
 |      :rtype: dict
 |  
 | ``` resolve_redirects(self, resp, req, stream=False, timeout=None, verify=True, cert=None, proxies=None, yield_requests=False, **adapter_kwargs)```
 |      Receives a Response. Returns a generator of Responses or Requests.
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors inherited from requests.sessions.SessionRedirectMixin:
 |  
 | ``` __dict__```
 |      dictionary for instance variables (if defined)
 |  
 |  ```__weakref__```
 |      list of weak references to the object (if defined)
 |  
 |  ----------------------------------------------------------------------

####   Methods inherited from docker.api.build.BuildApiMixin:

 |  
 | ``` build(self, path=None, tag=None, quiet=False, fileobj=None, nocache=False, rm=False, stream=False, timeout=None, custom_context=False, encoding=None, pull=False, forcerm=False, dockerfile=None, container_limits=None, decode=False,buildargs=None, gzip=False)```
 |  
 |  ----------------------------------------------------------------------

####   Methods inherited from docker.api.container.ContainerApiMixin:

 |  
 | ``` attach(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```attach_socket(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```commit(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```containers(self, quiet=False, all=False, trunc=False, latest=False, since=None, before=None, limit=-1, size=False, filters=None)```
 |  
 | ``` copy(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` create_container(self, image, command=None, hostname=None, user=None, detach=False, stdin_open=False, tty=False, mem_limit=None, ports=None, environment=None, dns=None, volumes=None, volumes_from=None,network_disabled=False,name=None, entrypoint=None, cpu_shares=None, working_dir=None, domainname=None, memswap_limit=None, cpuset=None, host_config=None,mac_address=None, labels=None, volume_driver=None, stop_signal=None, networking_config=None)```
 |  
 | `` create_container_config(self, *args, **kwargs)``
 |  
 |  ```create_container_from_config(self, config, name=None)``
 |  
 |  ```create_endpoint_config(self, *args, **kwargs)```
 |  
 |  ```create_host_config(self, *args, **kwargs)```
 |  
 | ``` create_networking_config(self, *args, **kwargs)```
 |  
 |  ```diff(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` export(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` get_archive(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` inspect_container(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` kill(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```logs(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` pause(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```port(self, resource_id=None, *args, **kwargs)```
 |  
skipping

####   Methods inherited from docker.api.exec_api.ExecApiMixin:
 |  
 | ``` exec_create(self, *args, **kwargs)```
 |  
 | ``` exec_inspect(self, *args, **kwargs)```
 |  
 |  ```exec_resize(self, *args, **kwargs)```
 |  
 | ``` exec_start(self, *args, **kwargs)```
 |  
 |  ----------------------------------------------------------------------

####   Methods inherited from docker.api.image.ImageApiMixin:

 |  
 | ``` get_image(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` history(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```images(self, name=None, quiet=False, all=False, viz=False, filters=None)```
 |  
 |  ```import_image(self, src=None, repository=None, tag=None, image=None, changes=None, stream_src=False)```
 |  
 |  ```import_image_from_data(self, data, repository=None, tag=None, changes=None)```
 |  
 |  ```import_image_from_file(self, filename, repository=None, tag=None, changes=None)```
 |  
 | ``` import_image_from_image(self, image, repository=None, tag=None, changes=None)```
 |  
 |  ```import_image_from_stream(self, stream, repository=None, tag=None, changes=None)```
 |  
 | ``` import_image_from_url(self, url, repository=None, tag=None, changes=None)```
 |  
 | ``` insert(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```inspect_image(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```load_image(self, data)```
 |  
 |  ```pull(self, repository, tag=None, stream=False, insecure_registry=False, auth_config=None, decode=False)```
 |  
 |  ```push(self, repository, tag=None, stream=False, insecure_registry=False, auth_config=None, decode=False)```
 |  
 | ``` remove_image(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```search(self, term)```
 |  
 | ``` tag(self, resource_id=None, *args, **kwargs)```
 |  
 |  ----------------------------------------------------------------------

####  Methods inherited from docker.api.network.NetworkApiMixin:

 |  
 |  ```connect_container_to_network(self, resource_id=None, *args, **kwargs)```
 |  
 |  ```create_network(self, *args, **kwargs)```
 |  
 |  ```disconnect_container_from_network(self, resource_id=None, *args, **kwargs)```
 |  
 |  ``inspect_network(self, *args, **kwargs)```
 |  
 |  ```networks(self, *args, **kwargs)```
 |  
 |  ```remove_network(self, *args, **kwargs)```
 |  
 |  ----------------------------------------------------------------------

####  Methods inherited from docker.api.service.ServiceApiMixin:

 |  
 | ``` create_service(self, *args, **kwargs)```
 |  
 |  ```inspect_service(self, *args, **kwargs)```
 |  
 | ``` inspect_task(self, *args, **kwargs)```
 |  
 | ```remove_service(self, *args, **kwargs)```
 |  
 |  ```services(self, *args, **kwargs)```
 |  
 |  ```tasks(self, *args, **kwargs)```
 |  
 |  ``update_service(self, *args, **kwargs)```
 |  
 |  ----------------------------------------------------------------------
 ####  Methods inherited from docker.api.swarm.SwarmApiMixin:
 |  
 | ``` create_swarm_spec(self, *args, **kwargs)```
 |  
 | ``` init_swarm(self, *args, **kwargs)```
 |  
 | ``` inspect_node(self, resource_id=None, *args, **kwargs)```
 |  
 | ``` inspect_swarm(self, *args, **kwargs)```
 |  
 | ``` join_swarm(self, *args, **kwargs)```
 |  
 | ``` leave_swarm(self, *args, **kwargs)```
 |  
 |  ```nodes(self, *args, **kwargs)```
 |  
 |  ```update_swarm(self, *args, **kwargs)```
 |  
 |  ----------------------------------------------------------------------
####  Methods inherited from docker.api.volume.VolumeApiMixin:
 |  
 |  ```create_volume(self, *args, **kwargs)```
 |  
 |  ```inspect_volume(self, *args, **kwargs)```
 |  
 |  ```remove_volume(self, *args, **kwargs)```
 |  
 |  ``volumes(self, *args, **kwargs)```