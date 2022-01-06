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
>> #### 1. Telgraf Metric 수집 다음 Plugin을 추가해준다.
  >>> <pre>
  >>> <code>
  >>> [[inputs.http_response]]
  >>>
  >>> urls = ["http://example.com]
  >>> HTTP Response Code를 응답받을 URL을 넣어준다.
  >>> 
  >>> HTTP Response의 응답 대기 시간
  >>> response_timeout = "5s" 
  >>>
  >>> method = "GET"
  >>> HTTP 요청방법
  >>></code>
  >>></pre>
>>#### 2. InfluxDB Data Transfer
>>#### 3. Grafana Query

>>> <pre>
>>> <code>
>>> 아래와 같은 Query를 추가해준다. (Grafana Query .txt 참고)
>>> from(bucket: "HTTP")
>>>  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
>>>  |> filter(fn: (r) => r["_measurement"] == "http_response")
>>>  |> filter(fn: (r) => r["_field"] == "http_response_code")
>>>  |> filter(fn: (r) => r["server"] == "https://aws.amazon.com/ko/console/" or r["server"] == "https://github.com/" or r["server"] == "https://hub.docker.com/" or r["server"] == "https://naver.com/" or r["server"] == "https://react.hxecorp.com/" or r["server"] == "https://www.google.com/" or r["server"] == "https://www.kakaocorp.com/" or r["server"] == "https://www.netflix.com/kr/")
>>> # 위 URL을 교체해준다. 
>>> # InfluxDB Explore에서 자신의 값을 선택한 뒤, 작업하면 편하다.
>>>  |> aggregateWindow(every: v.windowPeriod, fn: mean, createEmpty: false)
>>>  |> yield(name: "mean")
>>> </code>
>>> </pre>

>>#### 4. Grafana Dashboard
>>> Grafana 'json' Templete 참고
