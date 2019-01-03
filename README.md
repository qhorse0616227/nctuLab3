# Route Configuration

This repository is a lab for NCTU course "Introduction to Computer Networks 2018".

---
## Abstract

In this lab, we are going to write a Python program with Ryu SDN framework to build a simple software-defined network and compare the different between two forwarding rules.

---
## Objectives

1. Learn how to build a simple software-defined networking with Ryu SDN framework
2. Learn how to add forwarding rule into each OpenFlow switch

---
## Execution

> * How to run your program?  
   輸入指令：mn --custom topo.py --topo topo --link tc --controller remote //Run topo.py
   在另一個終端機輸入指令：ryu-manager controller.py –-observe-links  
   //Run controller.py  
   
> * What is the meaning of the executing command (both Mininet and Ryu controller)?  
   --custom 指定python檔  
   --topo 可以讓我們鍵入特定的拓墣模式及規格  
   --link 使用者可以對連線條件進行設定，所以使用者可以使用者進一步的設定頻寬、延遲時間等等  
   //ex.mn --link tc,bw=10,delay=10ms  
   --controller remote 遠端接上 OpenFlow Controller  
   
> * Show the screenshot of using iPerf command in Mininet (both `SimpleController.py` and `controller.py`)
   For SimpleController.py :  
   ![image](https://github.com/nctucn/lab3-qhorse0616227/blob/master/SimpleController_iPerf.png)  
   For controller.py :
   ![image](https://github.com/nctucn/lab3-qhorse0616227/blob/master/controller_iPerf.png)
---
## Description

### Tasks

> TODO:
> * Describe how you finish this work in detail

1. Environment Setup

2. Example of Ryu SDN

3. Mininet Topology

4. Ryu Controller

5. Measurement

### Discussion


1. Describe the difference between packet-in and packet-out in detail.  
   對於接受到的封包進行轉送到 Controller 的動作就稱為 packet-in。  
   對於接收到來自 Controller 的封包轉送到指定的port就稱為 packet-out。
   
2. What is “table-miss” in SDN?  
   一個packet在一個Flow Table裡沒有發現相對應的Flow Entry  

3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, MAIN_DISPATCHER)
    ```
   透過 set_ev_cls 裝飾器，依接收到的參數（事件類別、Switch與Controller之間的溝通狀況），而進行反應。  
   若以此圖為例，所代表的意思是負責 Packet-in 事件並Switch和Controller交握完畢的狀態  
   > * CONFIG_DISPATCHER：接收 SwitchFeatures  
   > * MAIN_DISPATCHER：一般狀態（交握完畢）  
   > * DEAD_DISPATCHER：連線中斷 //在此沒有用到  
   > * HANDSHAKE_DISPATCHER：交換 HELLO 訊息 //在此沒有用到  
   
5. What is the meaning of “datapath” in `controller.py`?
   
6. Why need to set "`ip_proto=17`" in the flow entry?
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.  
   controller.py 接收到的ACK比例比 SimpleController.py 還高  
   
8. Which forwarding rule is better? Why?  
   controller.py 較好

---
## References

* **I Read**
    * [Ryu-Simple Switch with Openflow 1.3](https://github.com/OSE-Lab/Learning-SDN/tree/master/Controller/Ryu/SimpleSwitch)
    * [撰寫 Ryu 簡易入門](https://github.com/OSE-Lab/Learning-SDN/tree/master/Controller/Ryu/FirstRyuApplication)
    * [交換器（ Switching Hub ）](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html)  
    * [OpenFlow Switch学习笔记(三)——Flow Tables](https://www.cnblogs.com/CasonChan/p/4620652.html)
* **Ryu SDN**
    * [Ryubook Documentation](https://osrg.github.io/ryu-book/en/html/)
    * [Ryubook [PDF]](https://osrg.github.io/ryu-book/en/Ryubook.pdf)
    * [Ryu 4.30 Documentation](https://github.com/mininet/mininet/wiki/Introduction-to-Mininet)
    * [Ryu Controller Tutorial](http://sdnhub.org/tutorials/ryu/)
    * [OpenFlow 1.3 Switch Specification](https://www.opennetworking.org/wp-content/uploads/2014/10/openflow-spec-v1.3.0.pdf)
    * [Ryubook 說明文件](https://osrg.github.io/ryu-book/zh_tw/html/)
    * [GitHub - Ryu Controller 教學專案](https://github.com/OSE-Lab/Learning-SDN/blob/master/Controller/Ryu/README.md)
    * [Ryu SDN 指南 – Pengfei Ni](https://feisky.gitbooks.io/sdn/sdn/ryu.html)
    * [OpenFlow 通訊協定](https://osrg.github.io/ryu-book/zh_tw/html/openflow_protocol.html)
* **Python**
    * [Python 2.7.15 Standard Library](https://docs.python.org/2/library/index.html)
    * [Python Tutorial - Tutorialspoint](https://www.tutorialspoint.com/python/)
* **Others**
    * [Cheat Sheet of Markdown Syntax](https://www.markdownguide.org/cheat-sheet)
    * [Vim Tutorial – Tutorialspoint](https://www.tutorialspoint.com/vim/index.htm)
    * [鳥哥的 Linux 私房菜 – 第九章、vim 程式編輯器](http://linux.vbird.org/linux_basic/0310vi.php)

---
## Contributors

> TODO:
> * Please replace "`YOUR_NAME`" and "`YOUR_GITHUB_LINK`" into yours

* [YOUR_NAME](YOUR_GITHUB_LINK)
* [David Lu](https://github.com/yungshenglu)

---
## License

GNU GENERAL PUBLIC LICENSE Version 3
