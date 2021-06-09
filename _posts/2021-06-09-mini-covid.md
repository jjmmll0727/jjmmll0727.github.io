---
title: "mini-covid"
excerpt: "simple toy project for self-training"
categories: "project"
---

<div style = "font-size: 28px; line-height: 25px;">
<center><strong>simple restful api project</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left;">
연합동아리 들어가기 전에 간단하게 nodejs를 유튜브를 보고 배웠었는데, 이 상태로 동아리에 들어가면 다른 팀원들에게 피해를 끼칠수도 있겠다는 생각을 했다. <br>
그래서 해당 동아리에서 활동 중인 선배님에게 간단하게 나마 restful api 프로젝트를 만들껀데 도와달라고 부탁을 했다. <br>
다행히도, 도와주셨고 전국의 코로나 인원을 매일 파악하여 알람으로 알려주는 아주 간단한 어플을 제작하였다. <br>
<br>
본격적으로 서버개발을 시작하게 된 프로젝트이어서 나에게 뜻깊다. <br><br><br>
<strong>전국의 코로나 인원을 크롤링하는 코드</strong>
</div>

```javascript
const request = require('request');
const cheerio = require('cheerio');
const baseUrl = 'http://ncov.mohw.go.kr/bdBoardList_Real.do?brdId=1&brdGubun=13&ncvContSeq=&contSeq=&board_id=&gubun=' 

const options = {
    url: baseUrl,
    headers: {
        'User-Agent': 'request'
    }
};
var count=0;
const crawling_all = () => { 
    return new Promise((resolve, reject) => {
        let region_infected = []
        request(options, ((error, response, body) => {
                if (!error && response.statusCode == 200) {
                    const $ = cheerio.load(body);
                    let region_src, new_infected_src;
                    for (let index = 2; index <= 19; index++){
                        const region = $(`#content > div > div.data_table.midd.mgt24 > table > tbody > tr:nth-child(${index}) > th`); // 지역
                        const new_infected = $(`#content > div > div.data_table.midd.mgt24 > table > tbody > tr:nth-child(${index}) > td:nth-child(2)`); // 전날 비교 증가한 감염자
                        
                        region.each((index, item) => {
                            region_src = `${$(item).text()}`;
                        });

                        new_infected.each((index, item) => {
                            new_infected_src = `${$(item).text()}`;
                        });
                        
                        region_infected.push({region : region_src, new_infected : new_infected_src});  
                        count++;
                    }
                    resolve(region_infected)
                } else {
                    reject('err')
                }
            })
        )
    })
}

module.exports = crawling_all;
```
<br>
<a href = "https://github.com/jjmmll0727/mini-covid119/tree/master/backend">github</a>