# array
关于js数组排序的一些常用算法

   //1.数组中奇数在前，偶数在后
   
    var this_arr= [1,2,3,4,5,6,7]; 
    var left=[];
    var right=[];
    for(var i=0;i<this_arr.length;i++){
        if(this_arr[i]%2==0){
            right.push(this_arr[i]);
        }
        if(this_arr[i]%2 !=0){
            left.push(this_arr[i]);
        }
        var sortArr=left.concat(right);
    }
    console.log("奇数在前偶数在后"+sortArr);

    //2.数组去重
    //方法一    下标判断
    function noRepeat(obj) {
        var new_arr = [];
        for (var i = 0; i < obj.length; i++) {
            if (new_arr.indexOf(obj[i]) == -1) {      //或==i
                new_arr.push(obj[i]);
            }
        }
        return new_arr;
    }

    var obj_arr2 = [0, 1, 3, 4, 6, 8, 9, 5, 3, 8, 21, 1,3,3,5,6,8];
    console.log('数组去重方法一:'+noRepeat(obj_arr2));


    //方法二  利用sort删除相邻相同项
    
    function removeRepeat(obj){
        obj.sort();                             //按顺序排序，相同数字的会在一起
        for(var i =0; i<obj.length;i++){
            if(obj[i]==obj[i+1]){
                obj.splice(i--,1);
            }
        }
        return obj; 
    }
    var obj_arr4=[1,2,2,3,21,8,3,2,5,44,33,2,1,33,33,8]
    console.log('数组去重方法二:'+removeRepeat(obj_arr4));



    //3.数字从大到小排序
    
    function sort(a,b) {
//        return a-b;             //升序
        return b-a;              //降序
    }

    var obj_arr3 = [0, 1, 3, 4, 6, 8, 9, 5, 3, 8, 21, 1];
    console.log('数字排序:'+obj_arr3.sort(sort));



    //4.计算数组中奇数和偶数的个数
    
    function countNum(obj){
        var odd=0;
        var even=0;
        for(var i=0;i<obj.length;i++){
           /* if(obj[i]%2==0){
                even++;
            }
            else{
                odd++;
            }*/
            obj[i]%2==0?even++ : odd++;
        }
    console.log('奇数个数为'+odd+'偶数个数为'+even);
        
    };
    var arr7=[0,1,2,3,4,5,6];
    countNum(arr7);


    //5.随机选取10到100之间的10个数字，并排序

    var _arr=[];
    function getRandom(iStart,iEnd){
        var iChoice=iEnd-iStart;
        return Math.floor(Math.random()*iChoice+10);       //random返回[0,1)之间数字    floor向下取整
    }
    for(var i=0;i<10;i++){
        _arr.push(getRandom(10,100));
    }

    console.log('随机选取10到100中十个数'+_arr)


    //6.首字母大写
    
    //方法一    substring
    function toUpper(str){
        var new_str=str.toLowerCase().split(" ");
        for(var i=0 ;i <new_str.length;i++){
            new_str[i]= new_str[i].charAt(0).toUpperCase()+new_str[i].substring(1);    //substring没有结束下标表示一直取到最后
        }
        var str=new_str.join("");
        return str;
    }
    var str2="we are friends";
    console.log('首字母大写'+toUpper(str2));                 



    //方法二  replace
     function toUpper2(str){
        var new_str=str.toLowerCase().split(" ");
        for(var i=0 ;i <new_str.length;i++){
           var firstLetter=new_str[i].charAt(0);
           new_str[i]=new_str[i].replace(firstLetter,function(firstLetter){
            return firstLetter.toUpperCase();
           })
        }
        var str=new_str.join("");
        return str;
    }

    var str3="l love coffee";
    console.log('首字母大写'+toUpper2(str3));          



    //7.判断字符串中出现最多次的字符,统计次数
    
      var str="lalwayssssswanttolearnmoreknowlledde";
      var json={};
      for(var i=0; i<str.length;i++){
        var word=str.charAt(i);
        if(json[word]){                                 //word为json中一个属性,如果存在
            json[word]++;                               //属性值+1
        }else{
            json[word]=1;
        }
      };

      var max=0;                                        //最多的次数
      var maxWord=null;                                 //出现最多的字符
      for(var key in json){                             
        if(max<json[key]){                              
            max=json[key];                              //max始终存储最大值
        };
      }

      //为了避免几个字符的次数一样
      for(var key in json){
        if (json[key]==max) {                           //如果属性值与最大值相等的
            maxWord=key;
         console.log("次数最多的字符是:"+maxWord+"次数为:"+max);
        };
      }


      //判断第一个偶数的位置
      var arr8=[1,5,7,4,8,7,11,33,4];
      for(var i=0;i<arr8.length;i++){
        var flag=true;
        if(arr8[i]%2==0){
            arr8[i].index=i;
            var firstEven=arr8[i];
            break;
        }
      }
      console.log("第一个偶数为："+firstEven+"第一个偶数的位置为："+i);


      //8.全部排列组合
      
      var count=0;  
      function show(arr) {  
        console.log("第"+ ++count+"种方法:"+arr);  
      }  
      function perm(arr) {  
        (function fn(source, result) {  
            if (source.length == 0)  
                show(result);  
            else 
                for (var i = 0; i < source.length; i++)  
                    fn(source.slice(0, i).concat(source.slice(i + 1)), result.concat(source[i]));  
            })(arr, []);  
        }  
        perm(["A", "B", "C", "D"]);  
