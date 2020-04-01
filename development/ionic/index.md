---
layout: post
title:  "ionic을 이용한 하이브리드 앱 개발 삽질의 후기"
subtitle: "#mobile application #ionic #cordova #angular #cross mobile #coding"
type: "google spreadsheet data, oauth2, CORS"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: "ionic/img/header.jpg"
order: 6
date: 2020-03-31
comments: true
---

급하게 앱 하나를 개발하면서 몇 일 동안 삽질을 했던 후기를 쓴다.

### oauth2
- oauth2는 social sns 로그인을 위한 것이다.
- google spread sheet 데이터를 가져올 때 oauth2가 꼭 있어야 하는 것은 아니다.
- 헤맸던 부분 중 하나는, url이다. 
다른 문서에 `url = https://spreadsheets.google.com/feeds/list/' + id + '/od6/public/values?alt=json` id와 public 사이에 od6 으로 되어 있었는데, od6은 첫번째 시트만을 의미하는건지 아닌지 아무튼 안된다. `Invalid query parameter value for grid_id`라는 에러가 난다. 
찾아보니 이 부분을 ${id}/1/public 으로 바꾸니 에러 없이 실행됐는데, 여기서 1이 grid_id를 의미한다. 
결론적으로 `url = https://spreadsheets.google.com/feeds/list/${id}/1/public/values?alt=json` 으로 사용하면 된다.
- 코드는 본의 아니게 Angular

```
import {Injectable} from '@angular/core';
import {HttpClient} from "@angular/common/http";
import 'rxjs/add/operator/map';

/*
  Generated class for the GoogleDrive provider.
  See https://angular.io/docs/ts/latest/guide/dependency-injection.html
  for more info on providers and Angular 2 DI.
*/
@Injectable()
export class GoogleDriveProvider {
  data: any = null;

  constructor(public http: HttpClient) {}

  load(id) {
    var url = `https://spreadsheets.google.com/feeds/list/${id}/1/public/values?alt=json`
    // don't have the data yet
    return new Promise(resolve => {
      // We're using Angular Http provider to request the data,
      // then on the response it'll map the JSON data to a parsed JS object.
      // Next we process the data and resolve the promise with the new data.
      this.http.get(url)
        // .map(res => res.json())
        .subscribe( data => {
          console.log( 'Raw Data', data );
          this.data = data['feed'].entry;
          
          let returnArray: Array<any> = [];
          if( this.data && this.data.length > 0 ) {
            this.data.forEach( ( entry, index ) => {
              var obj = {};
              for( let x in entry ) {
                if( x.includes('gsx$') && entry[x].$t ){
                  obj[x.split('$')[1]] = entry[x]['$t'];
                }
              }
              returnArray.push( obj );
            });
          }
          resolve(returnArray);
        });
    });
  }
}
```


<br><br><br>
### 안드로이드 애뮬레이터, 실제 디바이스에서는 proxy 설정이 안된다. 해봤는데 안됨. 어떤 외국인의 의견 참고.
The proxy is a thing started and run by the CLI. If you use ionic serve or livereload, the CLI is running in the background doing things - and the proxy. The app uses the IP and port of the proxy for these requests.

When you run the app properly on the device, the CLI is not involed - so there is no proxy.

If your app has CORS issues when running on the device, you have to fix those and can’t use the workaround with the proxy. Means, making sure the backend sends the correct headers etc.


<br><br>
### CORS 에러 
자주 만나는 친군데..... header 값을 이용해서 해결하거나 백엔드에 요청해서 수정했었다.
그런데 이번에 외부 API를 받아오는 부분인데, 안되서 고생했다. 결론은 jsonp요청으로 해결. 너무 간단해서 황당.
삽질의 끝은 늘 이모양이죠. header, params를 다 주소에 붙였다. 예시로 간단한 함수 첨부함.
```
getSites(): Observable<any> {
    return this.http.jsonp(`${Constant.API}/sites/list?api_key=${Constant.KEY}`, 'callback');
  }
```


<br><br>
### 안드로이드 http
Android Studio를 이용해서 애뮬레이터나 실제 기기에 테스트할 때, 배포할 때,
app/manifests/AndroidManifest.xml 에서 android:usesCleartextTraffic="true" 이부분을 꼭 넣어줘야 http 요청이 가능하다.
```
<application android:usesCleartextTraffic="true"  android:hardwareAccelerated="true" android:icon="@mipmap/ic_launcher" android:label="@string/app_name" android:supportsRtl="true">
        <activity android:configChanges=" ...
```


<br><br>
이것저것 시도를 많이 해봤는데, 우선 되서 너무 다행이고. 배고프다. 이제 밥 먹어야지. 안뇽. 