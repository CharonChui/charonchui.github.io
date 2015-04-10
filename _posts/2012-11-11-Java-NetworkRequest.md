---
layout: post
title: "����������������ܽ�"
description: "Java Network Request"
category: Java
tags: [Java]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---

����������������ܽ�
===

�������ݴ��䣬��Ϥ���̡߳�Socket�����̡���ϤTCP��UDP��HTTP��Э��

- �����̸�����       
	- ����ģ�ͣ�      
		- OSIģ��      
			- Ӧ�ò�      
			- ��ʾ��     
			- �Ự��      
			- �����      
			- �����       
			- �������Ӳ�        
			- �����       
		- TCP/IPģ��       
			- Ӧ�ò�       
			- �����         
			- ���ʲ�      
			- �����������      
	- ����ͨѶҪ��      
		- IP��ַ    
		- �˿ں�      
		- ����Э��   
	- ����ͨѶǰ�᣺   
		- �ҵ��Է�IP        
		- ����Ҫ���͵�ָ���˿ڡ�Ϊ�˱�ʾ��ͬ��Ӧ�ó������Ը���Щ����Ӧ�ó��������ֽ��б�ʾ�����ʾ�ͽж˿�      
		- ����ͨ�Ź�����������Ϊͨ��Э�飬������֯������ͨ��Э��TCP/IP       
		
- TCP��UDP������      
	- UDPЭ�飺     
		����������    
		ÿ�����ݱ��Ĵ�С��������64k��        
		��Ϊ�����������ӣ������ǲ��ɿ�Э��       
		����Ҫ�������ӣ��ٶȿ�      
	- TCPЭ�飺       
		���뽨�����ӣ��γɴ������ݵ�ͨ��         
		�������пɽ��д�����������      
		ͨ����������������ӣ��ǿɿ�Э��         
		���뽨�����ӣ�Ч�ʻ��Ե�        
		
		�������֣�        
		- ��һ�Σ������㣺��ô��       
		- �ڶ��Σ���ش��ڡ�           
		- �����Σ��ҷ�����Ŷ����֪�����ڡ�         
- Socket��        
	- Socket����Ϊ��������ṩ��һ�ֻ���        
	- ͨ�ŵ����˶���Socket       
	- ����ͨ����ʵ����Socket���ͨ��      
	- ����������Socket��ͨ��IO����         
	- ��Socket��Ҫ���Ǽ�ס���̣�������ĵ�����             
	
- UDP(User Datagram Protocol)���û�����Э��            
	- UDP������       
		��ҪDatagramSocket��DatagramPacket������ʵ��UDPЭ�鴫������       
		UDPЭ����һ�����������ӵ�Э�顣���������ӵ�Э��ָ������ʽͨ��ǰ������Է��Ƚ������ӣ����ܶԷ�����״̬��ֱ�ӷ������ݡ�     
	- UDPЭ�鿪�����裺     
		- ���Ͷˣ�         
			- ����DatagramSocket����          
			- �ṩ���ݣ��������ݷ�װ���ֽ������У�       
			- ����DatagramPacket���ݰ����������ݷ�װ�����У�ͬʱָ�����ն�IP�ͽ��ն˿�       
			- ͨ��Socket��������send���������ݰ����ͳ�ȥ��       
			- �ر�DatagramSocket��DatagramPacket����        
		- ���նˣ�           
			- ����DatagramSocket���񣬲�����һ���˿ڣ�         
			- ����һ���ֽ������һ�����ݰ���ͬʱ�������װ�����ݰ���          
			- DatagramPacket��receive�����������յ����ݴ��붨��õ����ݰ���      
			- ͨ��DatagramPacke�رյķ�������ȡ�������ݰ��е���Ϣ��       
			- �ر�DatagramSocket��DatagramPacket����       
	- UDPЭ���Demo(��������)��    
		- ���Ͷˣ�      
			{% highlight java %}
			class UDPSend {
				public static void main(String[] args) throws Exception {
					DatagramSocket ds = new DatagramSocket();
					byte[] buf = "����UDP���Ͷ�".getBytes();
					DatagramPacket dp = new DatagramPacket(
						buf,buf.length,InetAddress.getByName("192.168.1.253"),10000);
					ds.send(dp);
					ds.close();
				}
			}
			{% endhighlight %}
		- ���ն�
			{% highlight java %}
			class UDPRece {
				public static void main(String[] args) throws Exception {
					DatagramSocket ds = new DatagramSocket(10000);
					byte[] buf = new byte[1024];
					DatagramPacket dp = new DatagramPacket(buf,buf.length);
					ds.receive(dp);//�����Ͷ˷��͵����ݰ����յ����ն˵����ݰ���
					String ip = dp.getAddress().getHosyAddress();//��ȡ���Ͷ˵�ip
					String data = new String(dp.getData(),0,dp.getLength());//��ȡ����
					int port = dp.getPort();//��ȡ���Ͷ˵Ķ˿ں�
					sop(ip+":"+data+":"+port);
					ds.close();
				}
			}
			{% endhighlight %}
- TCP/IPЭ�飺Socket��ServerSocket        
	- ����TCPЭ�������ͨ�Ÿ�����        
		- TCP/IPͨ��Э����һ�ֱ��뽨�����ӵĿɿ�������ͨ��Э�顣����ͨ�����˸�����һ��Socket,�Ӷ���ͨ�ŵ�����֮���γ�����������·��      
		- ����������·һ�����������˵ĳ���Ϳ��Խ���ͨ�š�    
	- TCP/IPЭ�鿪�����裺       
		- �ͻ��ˣ�       
			- ����Socket���񣬲�ָ��Ҫ���ӵ������Ͷ˿ڣ�      
			- ��ȡSocket���е������OutputStream��������д�����У�ͨ�����緢�͸�����ˣ�          
			- ��ȡSocket���е������InputStream����ȡ����˵ķ�����Ϣ��         
			- �ر���Դ��          
		- ����ˣ�      
			- ����ServerSocket���񣬲�����һ���˿ڣ�         
			- ͨ��ServerSocket�����accept��������ȡSocket�������        
			- ʹ�ÿͻ��˶���Ķ�ȡ����ȡ�ͻ��˷��͹��������ݣ�          
			- ͨ���ͻ��˶����д����������Ϣ���ͻ��ˣ�         
			- �ر���Դ        
			
	- TCP/IPЭ���һ��Demo(����Ҫ���գ�)��          
		- �ͻ��ˣ�     
			{% highlight java %}
			class TCPClient {
				public static void main(String[] args) {
					Socket s = new Socket("192.168.1.253",10000);
					OutputStream os = s.getOutputStream();
					out.write("����TCP���͵�����".getBytes());
					s.close();
				}
			}
			{% endhighlight %}
		- ����ˣ�
			{% highlight java %}
			class TCPServer {
				public static void main(String[] args) {
					ServerSocket ss = new ServerSocket(10000);
					Socket s = ss.accept();

					String ip = s.getInetAddress().getHostAddress();
					sop(ip);

					InputStream is = s.getInputStream();
					byte[] buf = new byte[1024];
					int len = is.read(buf);
					sop(new String(buf,0,len));
					s.close();
					ss.close();
				}
			}
			{% endhighlight %}
		
- HTTPЭ�飺
	- HTTP��Hyper Text Transfer Protocol����д
	- ����W3C�ƶ���ά���ġ�Ŀǰ�汾Ϊ1.0��1.1
	- �ǿ���web�Ļ�ʯ���ǳ�����Ҫ
	-  �汾
		- 1.0�汾������״̬��Э�飬��һ������ֻ��Ӧһ��������Ӧ���˾͹رմ˴�����Ҫ���ٷ��������½������ӡ������Ӷ��ǱȽϺ���Դ�ġ�
		- 1.1�汾������״̬��Э�顣��������һ���������ӻ����Ϸ����������͵õ���ε���Ӧ���������ϴ�����ʱ�����ʱ�����������Զ��ϵ����ӣ�����ǳ�ʱ���ơ�
	- HTTPЭ�����ɣ�        
		- ���󲿷֣�         
			- �����У�           
				- GET / HTTP/1.1  ����������ʽGET �������Դ·����/ Э��汾�ţ�HTTP/1.1             
					- ����ʽ�����õ���GET��POST            
						- GET��ʽ��Ĭ�Ϸ�ʽ��ֱ���������ַ��           
							- �����ݳ������������С�url?username=abc&password=123          
							- �ص㣺����ȫ���г������ƣ�<1k           
						- POST��ʽ������ͨ����form method="post"����           
							- �����ݻ�����������С�           
							- �ص㣺��ȫ��û�г�������              
			- ������Ϣͷ��           
			- �������ģ���һ������֮���ȫ��������������             
		- ��Ӧ���֣�            
			- ��Ӧ�У�          
				- HTTP/1.1 200 OK    ������Э��汾��:HTTP/1.1 ��Ӧ��:200 ����:OK              
					- ��Ӧ�룺(ʵ���õ���30������,��������W3C������)              
					- ����������Ӧ�������             
					- ������Ӧ�룺            
						- 200��һ������            
						- 302/307:�������Դ·�������            
						- 304����Դû�б��޸Ĺ�         
						- 404����Դ������,�Ҳ�����Դ           
						- 500�������������д�	         
			- ��Ӧ��Ϣͷ��       
			- ��Ӧ���ģ�           
				- ��һ������֮���ȫ��������Ӧ���ģ��������ʾ�ľ��������е�����

		
----
- ���� ��charon.chui@gmail.com  
- Good Luck! 

	