---
title: HTML/JS学习笔记
date: 2022-12-14 21:32:44
tags:
---

- **自动刷新**  
    **checkbox**  
    ```
    <input type="checkbox" id="autoRefresh"> 自动刷新 
    ```

    **js**
    ```
    <script>
        var timmer;
        document.getElementById("autoRefresh").onclick = function(){
            if(this.checked){
                timmer = setInterval(autoRefresh,1000);
            }else{
                clearInterval(timmer);
            }
        };
        function autoRefresh(){
            $('#table').bootstrapTable('refresh');
        }
    </script>
    ```

- **Chart.js**  
    **数据可视化**  
    [参考视频](https://youtu.be/T9W7vv5n7e0)
    ```
    <canvas id="myChart" width="400" height="200"></canvas>

    if(myChart instanceof Chart){
        myChart.destroy();
    }
    var ctx = document.getElementById('myChart');
    var separation = rs.msg.separation,
    labels = Object.keys(separation)
    datas = [];
    for(var i = 0; i < labels.length; i++){
        datas.push(separation[labels[i]] / 1024 / 1024);
        labels[i] = timestampToTime(labels[i]);
    }
    console.log(datas);
    const data = {
        labels: labels,
        datasets: [{
            label: rows[0].client_mac,
            data: datas,
            backgroundColor: [      // 设置每个柱形图的背景颜色
                'rgba(255, 99, 132, 0.2)'
            ],
            borderColor: [     //设置每个柱形图边框线条颜色
                'rgb(255, 99, 132)'
            ],
            borderWidth: 1
        }]
    };
    const config = {
        type: 'bar', // 设置图表类型
        data: data,
        options: {
            scales:{
                y:{
                    title: {
                        display: true,
                        text: '流量 / MB'
                    }
                },
                x:{
                    title: {
                        display: true,
                        text: '时间'
                    }
                }
            }
        }
    };
    myChart = new Chart(ctx, config);
    ```