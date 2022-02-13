## 《Java8实战》笔记
### 一 Lambda表达式
####  1.行为参数化
**什么是行为参数化？** ： 行为参数化：让方法接受多种行为（或战略）作为参数，并在内部使用，来完成不同的行为。行为参数化可以帮助应对不对变化的需求。
**例子：** 就农场库存程序而言，实现一个从列表中删选红色苹果的功能：

1. List<Apple> filterRedApples(List<Apple> appleList){  
   ...  
   **if("red".equals(apple.getColor())**  
        .add(apple)  
       ...  
   }  
2. 如果想筛选更所颜色的苹果呢？比如绿色，黄色，暗红色。。。，可以！将颜色参数作为参数： 
  
    List<Apple> filterApplesByColor(List<Apple> appleList, *String color*){  
     **if(color.equals(apple.getColor())**  
      .add(apple)  
  }  
3. 如果又有新的需求：如果能区分苹果的重量就好了，比如筛选重量大于150克的苹果。OK，重新写一个方法：  
   List<Apple> filterApplesByWeight(List<Apple> appleList, *int weight*){  
     **if(apple.getWeight() > weight)**  
      .add(apple)  
  }    
4.以上，解决方案不错，但是复制了大部分代码，有点令人失望。如果某一天需要改变变量方法提升性能，所有的方法都得修改，代价太大。  
  所有，写一个总的筛选方法,并加上一个标志来区分对颜色和重量的查询：  
   List<Apple> filterApples(List<Apple> appleList, *String color, int weight, boolean flag*){  
     **if((flag &&  color.equals(apple.getColor()) ||  
          !flag && apple.getWeight() > weight))**  
      .add(apple)  
  }  
5. 以上方法是可行，但是真的很笨拙。  调用时：  List<Apple> greenApples = filterApples(appleList, "green", 100, true);  
  勉强应付了需求，如果需求又增加了，要筛选形状，产地，大小等属性，或者更复杂的查询，怎么办？
  **需要更高层次的抽象：对选择标准建模**：我们考虑的是苹果，需要根据apple的某些属性来返回一个Boolean值，我们称之为“谓词”。  
  我们定义一个接口：
      `public interface ApplePredicate{
           boolean test (Apple apple)
      }`
  
      
      
  
 
  
  
