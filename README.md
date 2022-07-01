# Spring-boot-modules
spring boot modules test



1.新建一個SpringStarterProject工程
  File-->New-->Spring Starter Project
  該工程將作為父工程,此時暫不對該專案架構進行變動,只將pom.xml中的打包方式改為pom,
  springboot的版本號改為1.4.7.RELEASE, <packaging>pom</packaging>.
  
 2.建立各個子模組工程
 在上一個工程上點選右鍵-->New-->Maven Module
 根據自己的要求建立好各個子模組,如dao,service,web等
 
 
 3.變動整個專案的目錄結構
 因為web專案作為外部訪問的入口,而model、dao、service以及demo父工程都不需要對外提供訪問,
 所以將demo中的Springboot啟動類SpringbootMultiDemoApplication.java和屬性檔案application.properties
 檔案遷移至web專案中相當於demo父工程與web子工程進行了目錄交換.
 
 4將demo中多餘的目錄清除,demo中不需要寫程式碼.model、dao、service的目錄結構不變.
 
 5.改寫pom檔案完成依賴關係
 model子工程不依賴任何專案無須改動
 dao子工程新增對model子工程的直接依賴
 service子工程新增對dao的直接依賴,間接依賴model
 web子工程直接依賴service間接依賴dao和model
 
 
 我們最終需要的是web專案對外提供訪問, 並且dao,service,model都將作為依賴包打到web專案生成的可執行jar包中，
 然後在伺服器上執行,此時需要對父工程的pom.xml檔案進行改動,配置如何打包等等,父工程pom.xml檔案
 
專案如何打包:
選中父工程-->右鍵-->Run As-->Maven Install,操作完成後會在各個子工程target資料夾中生成一個指定名稱的jar包,將這些jar包一個個拿出來解壓,會發現在同樣的BOOT-INF/lib目錄下,每個jar包中的東西不一樣,model子工程的jar包只包含父工程中Maven依賴的包,dao中多了一個model子工程依賴包,service子工程多了model和dao兩個依賴包,web工程則包含了所有的jar包.我們最終部署執行的就是web工程target目錄下的可執行jar包。

app/hello.json


  
  
