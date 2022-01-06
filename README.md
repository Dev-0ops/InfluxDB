InfluxDB
=============================
### InfluxDB를 통한 Monitoring 방법에 대하여 <br>


<img src="/Collect_Flow.png" width="600px" height="200px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
> ### Monitoring process 
> > **Telegraf : Metric collect agent <br>
> > InfluxDB : Database <br>
> > Grafana : Monitoring Visualize, Alert <br>**


HTTP Response Monitoring
---------------------------------
<img src="/Main_DashBoard.png" width="900px" height="450px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>

### HTTP Response Monitoring이란? 
-> **HTTP(HTTPS)의 상태를 확인하기 위한 실시간 확인 작업을 의미한다.**

이때, 상태확인에 대한 응답은 'HTTP_Response_Code'를 통해 처리한다.

* HTTP_Response_Code URL : [https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C](https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C)    
<br><br>
> ### 동작 방식은 다음과 같다.
>> #### 1. Telgraf Metric 수집
  >>> <pre>
  >>> <code>
  >>> public class BootSpringBootApplication {
  >>> public static void main(String[] args) {
  >>>   System.out.println("Hello, Honeymon");
  >>> }
  >>>}
  >>></code>
  >>></pre>
>>#### 2. InfluxDB Data 전송
>>#### 3. Grafana Query







