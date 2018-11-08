# GoogleMapAPI
GoogleMapAPI_JAVASCRIPT

## 참고
https://developers.google.com/maps/documentation/javascript/tutorial

## 목차

**[0. Get API key](#0)**

**[1. Marker Clustering](#1)**

**[2. Importing Data into Maps](#2)**

**[3. Visualizing Data](#3)**

**[4. Combining Data](#4)**

**[5. Mapping with Firebase](#5)**

**[6. Geolocation](#6)**  

**[7. Using MySQL and PHP with Maps](#7)**

## <a id="0"></a>0. Get API Key

[Google Cloud Platform Console](https://console.cloud.google.com/google/maps-apis?_ga=2.244970114.609975226.1541575485-318552150.1534833761)에서 API key를 받는다.  
이 API키를 사용할 때 github 사용하려면 꼭 private 모드로 사용하거나 API키 부분을 숨긴다.
<pre>google cloud 새 프로젝트 생성 > API키 생성 > 사용할 API 선택

- API키 생성 : API 및 서비스 > 사용자 인증 정보
- 사용할 API 선택 : Marketplace > 원하는 API 선택 : 본 프로젝트에서는 maps JavaScript API 선택 > 활성화
</pre>
나의 app (html파일)의 script 태그를 이용해서, google map API를 loading 한다.  

````javascript
    <script async defer src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap"
    type="text/javascript"></script>
````    

참고문헌 : https://developers.google.com/maps/documentation/javascript/get-api-key#key-restrictions

## <a id="1"></a>1. Marker Clustering

마커클러스터를 사용하여 map에 많은 수의 마커를 표시한다  
근접 거리의 마커를 클러스터에 결합하여 마커 표시 단순화 한다.  
사용 API : Maps JavaScript API [MarkerClusterer](https://github.com/googlemaps/v3-utility-library/tree/master/markerclusterer) library  

해당 API를 html에 loading하기 위해 script 태그로 불러온다.

````javascript
    <script src="https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/markerclusterer.js"></script>
````

처음에 google map API를 loading하면, 바로 callback=initMap에 의해서 initMap()함수가 실행된다.  

initMap()함수 안에서 해야할 것은 총 4가지 이다.


0. locations 변수 설정 (initMap() 밖에서)

    ````javascript
        var locations = [
        {lat: -31.563910, lng: 147.154312},
        {lat: -33.718234, lng: 150.363181},...]
    ````    
    
    marker가 표시할 위치에 대한 data를 locations 변수에 저장해 두었다.

1. google Map 객체 생성
   
    ````javascript
        var map = new google.maps.Map(document.getElementById('map'), {
          zoom: 3,
          center: {lat: -28.024, lng: 140.887}
        });
    ````

    map 객체의 속성 : zoom , center 


2. label 변수 설정

    ````javascript
        var labels = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    ````

    marker에 표시할 알파벳들을 String으로 담아 나중에 split을 이용해서 하나씩 가져온다.    
   
3. maker 객체 설정

    ````javascript
        var markers = locations.map(function(location, i) {
          return new google.maps.Marker({
            position: location,
            label: labels[i % labels.length]
          });
        });
    ````


    locations 변수안에 담긴 {lat, lng}로 저장된 객체들의 집합에서 요소 하나하나씩 접근한다. (location : 반환된 요소 , i : 반복 횟수)  
    이후 새로운 Marker 객체를 생성해서 반환하는데, 이 Marker객체의 postion과 label 속성을 설정해준다.  
    postion 속성 : lat과 lng 객체가 들어있다 (=location 요소)  
    label 속성 : labels String에서 1개의 char만 가져온다. (반복 횟수에 따라서 label이 정해진다.)

4. markercluster 객체 설정
   
    ````javascript
        var markerCluster = new MarkerClusterer(map, markers,
            {imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m'});
    ````

    새로운 makerclusterer 객체를 생성한다. 이때 객체는 3가지 속성을 갖는다.  
    map : markercluster를 적용할 googlemap 변수 저장  
    markers : markercluster를 적용할 마커들의 집합  
    imagePath : markerclusterer 라이브러리에 있는 이미지를 가져온다. (여기의 imagePath값을 자신만의 이미지로 수정이 가능하다.)

## <a id="2"></a>2. Importing Data into Maps
## <a id="3"></a>3. Visualizing Data
## <a id="4"></a>4. Combining Data
## <a id="5"></a>5. Mapping with Firebase
## <a id="6"></a>6. Geolocation
## <a id="7"></a>7. Using MySQL and PHP with Maps
