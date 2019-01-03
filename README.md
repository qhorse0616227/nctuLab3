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


1. Environment Setup  
   先進入自己的container `ssh –p 16227 root@140.113.195.69`    
   然後把需要的資料clone到自己的repository `git clone https://github.com/nctucn/lab3-qhorse0616227.git Route_Configuration`  

2. Example of Ryu SDN  
   先把位置cd到src/裡  
   然後用Mininet來執行SimpleTopo.py   
   `mn --custom SimpleTopo.py --topo topo --link tc --controller remote`  
   再打開另一個終端機一樣cd到src/裡  
   然後用Ryu manager來跑SimpleController.py  
   `ryu-manager SimpleController.py --observe-links`  
   跑出結果後先關掉mininet那個視窗（輸入exit）  
   然後再關掉SimpleController.py（先按 Ctrl-Z 再輸入 mn -c）  
   
3. Mininet Topology  
   先將SimpleTopo.py複製到topo.py `cp SimpleTopo.py topo.py`  
   然後依照topo.png的圖修改topo.py的code  
   最後依照Task 2的步驟執行topo.py和SimpleController.py  

4. Ryu Controller  
   先將SimpleController.py複製到controller.py `cp SimpleController.py controller.py`   
   然後依照投影片上的圖修改controller.py的code  
   

5. Measurement
   依照Task 2的步驟執行topo.py和SimpleController.py  
   然後用iPerf檢測loss的比例  
   再依照Task 2的步驟執行topo.py和controller.py  
   一樣用iPerf檢測loss的比例

### Discussion


1. Describe the difference between packet-in and packet-out in detail.  
   對於接受到的封包進行轉送到 Controller 的動作就稱為 packet-in。  
   對於接收到來自 Controller 的封包轉送到指定的port就稱為 packet-out。
   
2. What is “table-miss” in SDN?  
   一個packet在一個Flow Table裡沒有發現相對應的Flow Entry  

3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?  
   因為class才能繼承app_manager.RyuApp  
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, MAIN_DISPATCHER)
    ```
   透過 set_ev_cls 裝飾器，依接收到的參數（事件類別、Switch與Controller之間的溝通狀況），而進行反應。  
   若以此圖為例，所代表的意思是負責 Packet-in 事件並且是Switch和Controller交握完畢的狀態  
   > * CONFIG_DISPATCHER：接收 SwitchFeatures  
   > * MAIN_DISPATCHER：一般狀態（交握完畢）  
   > * DEAD_DISPATCHER：連線中斷 //在此沒有用到  
   > * HANDSHAKE_DISPATCHER：交換 HELLO 訊息 //在此沒有用到  
   
5. What is the meaning of “datapath” in `controller.py`?  
   the switch in the topology using OpenFlow
   
6. Why need to set "`ip_proto=17`" in the flow entry?  
   使用UDP協定
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.  
   controller.py loss的比例比 SimpleController.py 還低  
   
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

* [Ting-yu Chen](https://github.com/qhorse0616227)
* [David Lu](https://github.com/yungshenglu)

---
## License

GNU GENERAL PUBLIC LICENSE Version 3
