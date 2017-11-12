实验三：利用分组嗅探器分析传输层与网络层协议
【实验前需要学习掌握的知识】
1、详细掌握TCP段结构。
 
2、详细掌握UDP段结构。
 
3、IP数据报结构
 
【实验目的】
1、了解传输层TCP/UDP协议构造；
2、了解网络层IP协议构造；
【实验内容】
1、对传输层协议TCP/UDP进行捕包分析并回答问题  
俘获大量的由本地主机到远程服务器的TCP传输
(1)启动浏览器，打开http://gaia.cs.umass.edu/ethereal-labs/alice.txt网页，得到ALICE'S ADVENTURES IN WONDERLAND文本，将该文件保存到你的主机上。
(2)打开http://gaia.cs.umass.edu/ethereal-labs/TCP-ethereal-file1.html
窗口如下所示。
 
在Browse按钮旁的文本框中输入保存在你的主机上的文件ALICE'S ADVENTURES IN WONDERLAND的全名（含路径），此时不要按“Upload alice.txt file”按钮
(3)启动Ethereal，开始分组俘获。
(4)在浏览器中，单击“Upload alice.txt file”按钮，将文件上传到gaia.cs.umass.edu服务器，一旦文件上传完毕，一个简短的贺词信息将显示在你的浏览器窗口中。
(5)停止俘获。
浏览追踪信息
(1)在显示筛选规则中输入“tcp”,你可以看到在你的主机和服务器之间传输的一系列的tcp和http报文，你应该能看到包含SYN报文的三次握手。也可以看到有你的主机向服务器发送的一个HTTP POST报文和一系列的“http continuation”报文。
(2)根据操作回答“实验报告”中的1-2题。
TCP基础
根据操作回答“实验报告”中的3-9题
TCP拥塞控制
(1)在Ethereal已俘获分组列表子窗口中选择一个TCP 报文段。选择菜单： Statistics->TCP Stream Graph-> Time-Sequence-Graph(Stevens)。你会看到如下所示的图。
 
根据操作回答“实验报告”中的10-11题。
2、对网络层协议IP进行捕包分析
注意分析网络层发送方和接收方IP地址关系，推荐采用对tracert命令进行捕包分析。
【实验方式】实验指导教师讲解演示，每位同学上机实验，并与指导教师讨论。
【实验地点】学院实验室。
下载共享版本http://www.pingplotter.com/安装pingplotter标准版（你有一个30天的试用期），通过对你所喜欢的站点执行一些traceroute来熟悉这个工具。ICMP回复请求消息的大小可以在pingplotter中设置：Edit->Options->Packet，在packet size字段中默认包的大小是56字节。pingplotter发送一系列TTL值渐增的包时，Trace时间间隔的值和间隔的个数在pingplotter中能够设置。按下面步骤做：
1．打开Ethereal，开始包捕获，然后在Ethereal包捕获的选择屏幕上点击OK；
2．开启pingplotter，然后在“Address to Trace”窗口输入目的地目标的名字：
在“#of times to Trace”区域输入3。然后选择Edit->Options->Packet，确认在packet size字段的值为56，点OK。然后按下Trace按钮。
3.接下来，发送一组具有较长长度的数据包，通过Edit->Options->Packet在包大小区域
输入值为2000，点OK。接着按下Resume按钮；
4.再发送一组具有更长长度的数据包，通过Edit->Options->Packet在包大小区域输入值
为3500，点OK。接着按下Resume按钮；
5.然后我们停止Ethereal tracing；
根据操作回答“实验报告”中的12-25题
在实验的基础上，回答以下问题：(请在实验报告中TCP与IP各5道题回答)
(1)	向gaia.cs.umass.edu服务器传送文件的客户端主机的IP地址和TCP端口号是多少？
(2)	Gaia.cs.umass.edu服务器的IP地址是多少？对这一连接，它用来发送和接收TCP报文段的端口号是多少？
(3)	客户服务器之间用于初始化TCP连接的TCP SYN报文段的序号（sequence number）是多少？在该报文段中，是用什么来标示该报文段是SYN报文段的？
(4)	服务器向客户端发送的SYNACK报文段序号是多少？该报文段中，ACKnowledgement字段的值是多少？Gaia.cs.umass.edu服务器是如何决定此值的？在该报文段中，是用什么来标示该报文段是SYNACK报文段的？
(5)	包含HTTP POST命令的TCP报文段的序号是多少？
(6)	考虑在TCP连接中含有HTTP POST并把它作为第一个片段的TCP片段。在TCP连接（包括含有HTTP POST的片段）中最先的六个片段的序列号是多少？每一个片段是什么时候发送的？每一个片段接收到ACK是什么时候？请给出每一个TCP片段发送和确认被收到时的间隔，即六个片段中的每一个RTT值是多少？当接收到每一个ACK时的EstimatedRTT值是多少？假设对于第一个片段来说，EstimatedRTT值和标准的RTT值相同。
EstimatedRTT=(1-α)*EstimatedRTT+α*SampleRTT （假设α＝0.125）可以知道如何计算即可
(7)	前六个TCP报文段的长度各是多少？
(8)	在整个跟踪过程中，接收端公示的最小的可用缓存空间是多少？限制发送端的传输以后，接收端的缓存是否仍然不够用？
(9)	在跟踪文件中是否有重传的报文段？进行判断的依据是什么？
(10)	利用Time-Sequence-Graph(Stevens) plotting工具，浏览由客户端向服务器发送的报文段序号和时间对应关系图。你能否辨别出TCP慢启动阶段的起止，以及在何处转入避免拥塞阶段？
(11)	阐述所测量到的数据与TCP理想化的行为有何不同？
(12)	选择你的电脑所发送的第一个ICMP请求消息，在包详细信息窗口扩展包的Internet协议部分。你的电脑的IP地址是多少？
(13)	在IP包头部，上层协议区域的值是多少？
(14)	IP头部有多少字节？IP数据包的有效载荷是多少字节？解释你是怎样确定有效载荷的数量的？
(15)	这个IP数据包被分割了吗？解释你是怎样确定这个数据包是否被分割？
接下来单击列名按IP源地址排序数据包，选择你的电脑发送的第一个ICMP请求消息，扩展显示IP协议的数据。
(16)	在包捕获列表窗口，你能看到在第一个ICMP下的所有并发的ICMP消息吗？
(17)	往同一IP的数据包哪些字段在改变，而且必须改变？为什么？哪些字段是保持不变的，而且必须保持不变？
(18)	描述一下在IP数据包的Identification字段的值是什么样的？
接下来找到通过最近的路由器发送到你的电脑去的ICMP的TTL溢出回复的系列，回答以下问题：
(19)	Identification字段和TTL字段的值是多少？
(20)	所有的通过最近的路由器发送到你的电脑去的ICMP的TTL溢出回复是不是值都保持不变呢？为什么？
接下去研究一下分片，先按时间顺序排序数据包，找出在pingplotter中把包的大小改成2000后，你的电脑所发送的第一个ICMP请求消息。回答以下问题：
(21)	那个消息是否传送多于一个IP数据包的分片？看第一个被分割的IP数据包的片段，在IP头部有什么信息指出数据包已经被分割？在IP头部有什么信息指出这是否是第一个与后面片段相对的片段？这个IP数据包的长度是多少？
(22)	看被分割的IP数据包的第二个片段。在IP头部有什么信息指出这不是第一个数据包片段？有更多的片段吗？你是怎么知道的？和上一个分片的长度加起来是2000吗？
(23)	哪个字段在第一个和第二个片段之间的IP头部改变了？Identification变了吗
再找出在pingplotter中把包的大小改成3500后，你的电脑所发送的第一个ICMP请求消息。回答以下问题：
(24)	从原始的数据包中产生了多少片段？片偏移分别为多少？
(25)	在片段之中IP头部哪些字段改变了？Identification变了吗？

