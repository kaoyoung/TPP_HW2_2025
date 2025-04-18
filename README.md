# TPP_HW2_2025
## Main Idea
We think we may category the action of a player into three main parts. 
1. Predicting the action of the partner
2. Determing which order that ze wants to do
3. According to the order and the map information, deciding which food make first 

## The class we create
### Order class
In this class we provide the information about the order mainly focus on the priority about the orders. We think that the priority of the order is effected by three parts 
1. The distance of finishing the whole order.
2. The price of the order. <br/>
~~Note that we may think distance as how hard to finish that order, that is not limited to the geograph distance(you may add the extra cost of the object that ze encounters in the whole path)~~.<br/>
需實做出兩距離函式<br/>
```cpp
float BFS()
```
```cpp
float manhattan()
```
依照距離和order價格給出order的priority。 <br/>
```cpp
vector<int> priority(); // return the order according to the prority
```
這函數依據priority回傳order，由大到小排序。<br/>
例子 : 1號訂單priority 15；2號訂單priority 25; 3號訂單priority 20。 回傳(2,3,1) <br/>

### Map class 
In this class we provide the information about the map mainly focus on finding the positoin of the certain object. 
This class will provide two functions 
1. vector<pair<int, int>> FindObject(string object)
2. pair<int, int> FindNearestObject(string object)

```cpp
vector<pair<int, int>> FindObject(string object);     // return the object postion in the map
```
給定object後回傳該object在的位置。
object的輸入只能為plyer class提到的objectNames陣列中的元素，objectNames陣列以外的一律return make_pair(-1, -1)且輸出如下錯誤
```cpp
cerr << "we are finding the invalide object" << endl;
```


```cpp
pair<int, int> FindNearestObject(string object);     // return the object postion in the map
```
距離函式在初始化須給定，不然為預設的mahannton distance
給定object後回傳離player最近的object在的位置。
object的輸入只能為objectNames陣列中的元素，objectNames陣列以外的一律return make_pair(-1, -1)且輸出如下錯誤
```cpp
cerr << "we are finding the invalide object" << endl;
```

### Partner class 
In this class we provide the information about the partner mainly focus on predicting the order that partner makiing. 
According to the food holding by the partner to determind the order ze might be makeing.

### Player class 
In this class we provide the information about the player mainly focus on the action about the player according to the given order.
```cpp
constexpr int foodCount = 5;
constexpr char* foodNames[foodCount] = {"TART", "CROISSANT", "CHOPPED_STRAWBERRIES", "ICE_CREAM", "BLUEBERRIES"}; // how about using enum

constexpr int ingredientCount = 4;
constexpr char* ingredientNames[ingredientCount] = {"DOUGH", "CHOPPED_DOUGH", "RAW_TART", "STRAWBERRIES"}; // how about using enum

constexpr int objectCount = 14;
constexpr char* objectNames[objectCount] = {"TART", "CROISSANT", "CHOPPED_STRAWBERRIES", "ICE_CREAM", "BLUEBERRIES", 
                                            "DOUGH", "CHOPPED_DOUGH", "RAW_TART", "STRAWBERRIES",
                                            "DISHWASHER", "WINDOW", "CHOPPING_BOARD", "OVEN",
                                            "EMPTY"}; // how about using enum； EMPTY is empty table
```

This class provides five functions 
```cpp
string NeededFood();     // return the food that needed to finish the order orderIndex (exclude dish)
```
這函數在給定訂單號碼後，可回傳還需要的食物 
回傳例子 : TART-CROISSANT-CHOPPED_STRAWBERRIES
需要 : map中的find函式

```cpp
float ObjectDistance(string object); // return the distance between object and you
```
距離函式在初始化須給定，不然為預設的mahannton distance
這函數在給定object後，可回傳到object的距離

```cpp
map<string, float> IngredientOrder(); // return the ingredient order according to the distance() from small to high
```
距離函式在初始化須給定，不然為預設的mahannton distance
這函數在給定訂單號碼後，回傳還未出現在場上的食物的食材並依據到玩家的distance由小到大排好()

```cpp
bool CanFinshOrder();
```
這函數在給定訂單號碼後，回傳是否能由在場上的食物完成該訂單。


```cpp
map<string, float> FoodOrder(); // return the food order according to the distance() from small to high
```
距離函式在初始化須給定，不然為預設的mahannton distance
這函數在給定訂單號碼後，回傳出現在場上的食物並依據到玩家的distance由小到大排好()

```cpp
bool PickUpFood(string object); // help user pick up the food or ingredient by USE provided by the game; return true if object exist, false if object doesn't exist
```
距離函式在初始化須給定，不然為預設的mahannton distance
這函數在給定object後，可自動用USE幫你用該object，一樣使用距離函式幫你找最近的，object的輸入為 objectNames陣列中的元素。



## Example
