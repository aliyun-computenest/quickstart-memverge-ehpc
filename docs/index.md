MemVerge服务计算巢模式部署文档 
========================================
>**免责声明：**本文档可能包含第三方产品信息，该信息仅供参考。阿里云对第三方产品的性能、可靠性和操作可能带来的潜在影响，不做任何暗示或其他形式的承诺。

概述 
-----------------------

MemVerge Memory Machine是全球第一个大内存软件。它可以将DRAM和PMEM进行虚拟化，实现无需更改代码即可访问新的PMEM内存介质，以提供实时分析和AI/ML应用程序所需的大规模内存容量。同时提供了业内第一个企业级的内存数据服务，实现对高可用内存的企业级数据服务，支持宕机恢复的快照和复制功能。本文介绍部署MemVerge服务实例的详细信息。
[视频地址](https://cloud.video.taobao.com/play/u/null/p/1/e/6/t/1/d/ud/368971096225.mp4)

使用说明 
-------------------------

本文介绍了部署MemVerge服务实例的整体流程。

1. 登录阿里云账号，若您是通过RAM账号登录，请检查RAM账号权限。

   若缺少权限请登录主账号或者有RAM管理权限的账号添加。详细操作，请参见[RAM账号所需权限](#section-zgw-x4d-s6i)。

2. 一键为EHPC产品授予访问您云资源的权限。

   为EHPC产品授权的详细操作，请参见[授予弹性高性能集群（EHPC）访问权限](#section-bcr-1jv-xb3)。

3. 进入计算巢控制台，在推荐服务中找到Memory Machine-ehpc版，点击创建服务实例进入部署页面，或者从服务商处获取部署链接进入部署页面，填写相应参数。

   填写服务实例详细参数的具体信息，请参见[MemVerge服务实例部署流程](#section-hte-9yk-wts)。

4. 资源部署完成后，您可以通过公网IP访问应用GUI，并通过命令行检查计算节点服务是否正常启动。

   测试MemVerge Memory Machine的详细操作，请参见[验证MemVerge Memory Machine](#section-zol-7dh-vtx)。

5. 联系服务商获取并激活许可证，激活后登录软件进行使用。

   使用MemVerge Memory Machine的详细信息，请参见[使用MemVerge Memory Machine](#section-aje-62u-9c0)。




上述流程的图示如下。
![流程图](images/p460167.png)

RAM账号所需权限 
------------------------------

MemVerge服务需要对部分阿里云资源进行访问和创建操作，若您使用RAM账号创建服务实例，则需要在创建服务实例前，确认该RAM账号是否包含下表中的权限。查看RAM用户权限的详细操作，请参见[查看RAM用户的权限](https://help.aliyun.com/document_detail/145198.html)。

若缺少权限，请登录阿里云主账号或者有RAM管理权限的账号添加权限后，再部署服务实例。添加RAM权限的详细操作，请参见[为RAM用户授权](https://help.aliyun.com/document_detail/116146.html)。


|        权限策略名称        |         备注         |
|----------------------|--------------------|
| AliyunNASFullAccess  | 管理文件存储服务（NAS）的权限   |
| AliyunECSFullAccess  | 管理云服务器服务（ECS）的权限   |
| AliyunVPCFullAccess  | 管理专有网络（VPC）的权限     |
| AliyunEHPCFullAccess | 管理弹性高性能计算（EHPC）的权限 |



授予弹性高性能集群（EHPC）权限 
----------------------------------------

部署服务实例前，请使用阿里云主账号登录弹性高性能集群（EHPC）的[云资源访问授权](https://ram.console.aliyun.com/role/authorize?request=%7B%22ReturnUrl%22%3A%22https%3A%2F%2Fehpc.console.aliyun.com%22%2C%22Services%22%3A%5B%7B%22Roles%22%3A%5B%7B%22RoleName%22%3A%22AliyunEHPCDefaultRole%22%2C%22TemplateId%22%3A%22DefaultRole%22%7D%5D%2C%22Service%22%3A%22EHPC%22%7D%5D%7D)页面，单击 **同意授权** 。授权后，弹性高性能集群（EHPC）将获取对您云资源相应的访问权限。

若您未授予访问权限，创建弹性高性能集群（EHPC）时，会报无权限的错误导致服务实例部署失败。
![授权](images/p456666.png)

MemVerge服务实例部署流程 
-------------------------------------

**部署步骤**

1. 登录[计算巢控制台](https://computenest.console.aliyun.com/user/cn-hangzhou/recommendService)，在 **推荐服务** 页，找到 **Memory Machine-ehpc版** 服务。

2. 单击 **创建服务实例** 或者直接从服务商处获取部署链接。进入服务实例部署页面。按照流程指引填写相关参数，完成服务实例部署。

   服务实例部署完成后，服务器资源和软件一起生成。
   




**部署参数说明**

您在创建服务实例的过程中，需要配置服务实例信息，下表介绍MemVerge服务实例部署需要配置的详细参数及注意事项。


|    名称    |   类型   | 是否必填 |      默认值      |                                                                可选值                                                                 |                                                                                                                  说明                                                                                                                   |
|----------|--------|------|---------------|------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 地域       | String | 是    | 华东1（杭州）       | 华北2（北京）、华北3（张家口）、华东1（杭州）、华东2（上海）                                                                                                   | 资源所在的区域，目前只支持带有re6p系列机型的地域。                                                                                                                                                                                                           |
| 集群名称     | String | 是    | 无             | 无                                                                                                                                  | EHPC集群的名称。长度为2-64个字符。                                                                                                                                                                                                                 |
| 集群登录密码   | String | 是    | 无             | 无                                                                                                                                  | 集群的访问密码。长度为8-30个字符，且必须包含三项（大写字母、小写字母、数字、 ()\`\~!@#$%\^\&\*_-+=\|{}\[\]:;'\<\>,.?/ 中的特殊符号）。                                                                                                                                            |
| Ehpc部署模式 | String | 是    | Tiny          | Tiny Sample Standard                                                                                               | Ehpc部署模式包含三种模式。其中 **Tiny** 模式下，计算节点配置中包含登录节点和计算节点的信息，需要单独配置一个管控节点。 其他模式下有专用登录节点、计算节点和管控节点。                                                                                                                                            |
| 计算节点实例类型 | String | 是    | 无             | ecs.re6p.large ecs.re6p.xlarge ecs.re6p.2xlarge ecs.re6p.4xlarge ecs.re6p.13xlarge | 仅支持持久内存型re6p系列的实例，推荐配置为ecs.re6p.xlarge。                                                                                                                                                                                               |
| 计算节点数量   | Number | 是    | 1             | 1-99                                                                                                                               | 计算节点的实例数量。 * 部署模式为Tiny模式时，推荐配置1台ECS计算节点。  * 部署模式为simple模式时，推荐配置2台ECS计算节点。  * 部署模式为standard模式时，推荐配置3台ECS计算节点。   |
| 登录节点实例类型 | String | 是    | 无             | 所有ECS可用实例类型                                                                                                                        | 登录节点的实例类型，通常对机器配置要求较低，选择满足需求即可。 部署模式为Tiny模式时，无此选项。                                                                                                                                                                                    |
| 登录节点数量   | Number | 是    | 1             | 1-8                                                                                                                                | 登录节点的实例数量。 部署模式为Tiny模式时，无此选项。                                                                                                                                                                                                         |
| 管控节点实例类型 | String | 是    | 无             | 所有ECS可用实例类型                                                                                                                        | 管控节点的实例类型。                                                                                                                                                                                                                            |
| 管控节点数量   | Number | 是    | 1             | 1-8                                                                                                                                | 管控节点的实例类型。                                                                                                                                                                                                                            |
| 系统盘类型    | String | 是    | 无             | ESSD云盘 高效云盘 SSD盘                                                                                                   | 选择系统盘的类型。                                                                                                                                                                                                                             |
| 系统盘大小    | Number | 是    | 40 GB         | 无                                                                                                                                  | 选择系统盘的大小，单位为GB。                                                                                                                                                                                                                       |
| OSTag    | String | 是    | CentOS_7.6_64 | CentOS_7.6_64 CentOS_7.9_64                                                                                        | 自定义镜像。                                                                                                                                                                                                                                |
| 调度器类型    | String | 是    | Pbs           | Pbs slurm                                                                                                                          | 调度器类型，当前仅支持pbs和slurm两种类型。                                                                                                                                                                                                             |
| 域账户服务类型  | String | 是    | Nis           | Nis ldap                                                                                                                           | 域账户服务类型， 当前仅支持nis和ldap两种类型。                                                                                                                                                                                                           |
| 可用区      | String | 是    | 无             | 无                                                                                                                                  | 选择新建ECS实例的可用区。                                                                                                                                                                                                                        |
| 交换机ID    | String | 是    | 无             | 无                                                                                                                                  | 选择现有网络交换机的实例ID。                                                                                                                                                                                                                       |
| 付费类型     | String | 是    | 按量付费          | 按量服务 预付费（包年包月）                                                                                                                     | 选择服务实例的付费类型。                                                                                                                                                                                                                          |
| 文件系统类型   | String | 是    | standard      | standard extreme                                                                                                                   | 选择NAS文件系统。                                                                                                                                                                                                                            |
| 文件系统协议类型 | String | 是    | nfs           | nfs nfs3 nfs4                                                                                                      | 选择文件系统协议的类型。                                                                                                                                                                                                                          |
| 文件系统ID   | String | 是    | 无             | 无                                                                                                                                  | 选择NAS实例ID。                                                                                                                                                                                                                            |
| 挂载点      | String | 是    | 无             | 无                                                                                                                                  | 选择NAS挂载点。                                                                                                                                                                                                                             |



验证MemVerge Memory Machine 
----------------------------------------------

服务实例部署完成后，MemVerge Memory Machine也会自动完成安装部署。您需要测试Memory Machine服务的GUI和计算节点是否正常启动。测试方法如下：

1. **测试GUI是否正常启动**

   您可以使用如下两种方式中的任一一种进行测试。
   * 登录[阿里云弹性高性能计算控制台](https://ehpc.console.aliyun.com/#/cluster?regionId=cn-shenzhen)，找到MemVerge部署集群的公网IP地址，通过http://公网IP:8081链接访问8081端口，若能正常启动GUI登录页面，则表示GUI已经正常启动；若未正常启动，则可以通过support@memverge.com联系MemVerge服务商，寻找技术支持。![方法一](images/p459352.png)
   
   * 在计算巢控制台，找到部署的服务实例，进入服务实例详情页，单击 **VisitUrl** 后的IP地址，打开Memory Machine Management Center界面。若能正常启动GUI登录页面，则表示GUI已经正常启动；若未正常启动，则可以通过support@memverge.com联系MemVerge服务商，寻找技术支持。![方法二](../images/p459353.png)
   

   

2. **测试计算节点服务是否正常启动**
   1. 登录[阿里云弹性高性能计算控制台](https://ehpc.console.aliyun.com/#/cluster?regionId=cn-shenzhen)，单击 **集群** 页右上方的 **远程连接** 。![远程连接](images/p459355.png)
   
   2. 在弹出的 **远程连接** 弹框中，输入 **集群用户名** 、 **登录密码** 和 **端口** 信息后单击 **SSH连接** ，进入命令行工具mvmcli。

      集群用户名为root，登录密码为部署过程中设置的集群密码，端口默认填写22。
      ![远程连接](images/p459540.png)
   
   3. 在阿里云弹性高性能控制台左侧导航栏，选择 **资源管理** \> **节点与队列** 。
   
   4. 在 **集群** 框中，选择您创建的集群名称，在 **节点类型** 框中，选择计算节点。
   
   5. 在 **节点列表** 中，获取节点的IP地址，在命令行工具中运行ssh root@私网 IP，登录计算节点。![获取私有IP地址](images/p459855.png)
   
   6. 登录计算节点后，先输入`/usr/local/share/memverge/sbin/mvmcli show-usage`命令，执行后，再输入`systemctl status mvmallocd`命令。查看执行结果。

      执行结果如下图所示，表示服务正常启动。![回显结果](images/p459457.png)

      若Pmem显示为0，或者出现下图所示结果时，表示服务未成功启动。请通过support@memverge.com联系MemVerge服务商，寻找技术支持。
      ![错误回显](images/p459463.png)
   

   




使用MemVerge Memory Machine 
----------------------------------------------

测试通过后，您可以通过support@memverge.com邮箱或访问[MemVerge](https://market.aliyun.com/store/4925597.html#/)联系MemVerge服务商。服务商的售前工程师会收集您的机器信息，协助您登录并激活Memory Machine Management Center的License。

激活Memory Machine Management Center后，您就可以登录查看资源情况和使用软件。
![查看资源](images/p459523.png)
