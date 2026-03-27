---
title: leetcode
date: 2022-12-18 23:18:56
published: false
---





# 数组

## 两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

来源：力扣（LeetCode）

```
 public static void main(String[] args) {
       int[] nums = {3,2,4};
       int target = 6;
        System.out.println(Arrays.toString(twoSum(nums, target)));
    }

方法一:
    public static int[] twoSum(int[] nums, int target) {
        int[] newNums= new int[2];
        // 第一次遍历，需要循环多少次
        for (int i = 0; i < nums.length; i++) {
            for (int j = i+1; j < nums.length; j++) {
                // 判断第一次循环的i和第二次循环的j进行相加等于target
                if (nums[i]+nums[j]==target){
                    //存入数据到新数据中
                    newNums[0]= i;
                    newNums[1] = j;
                }
            }
        }
        return newNums;
    }));
        
        
方法二:
  Map<Integer, Integer> hashtable = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; ++i) {
            // containsKey检查key是否存在，第一次循环key肯定是不存在，如果存在证明集合中的key+当前nums[i]等于target
            if (hashtable.containsKey(target - nums[i])) {
                return new int[]{hashtable.get(target - nums[i]), i};
            }
            // 给hashMap中存入数据key是当前的值，值是当前索引
            hashtable.put(nums[i], i);
            System.out.println(hashtable);
        }
        return new int[0];

        
```

## 盛最多水的容器

给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

说明：你不能倾斜容器。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

![image-20221225130224012](D:\project\blogImage\image-20221225130224012.png)

```
package leetcode;

public class Solution {
    public static void main(String[] args) {
        System.out.println(maxArea(new int[]{1,8,6,2,5,4,8,3,7}));
    }

//    盛最多水的容器
    public static int maxArea(int[] height) {
       // 定义两个变量，使用双指针
        int start=0;
        int end = height.length-1;
        //在定义一个变量，记录容器的面积
        int rectangle = 0;
        while (start!=end){
            if (height[start]>=height[end]) {
                rectangle = Math.max(rectangle,Math.min(height[start],height[end])*(end-start));
                end--;
            }else {
                rectangle = Math.max(rectangle,Math.min(height[start],height[end])*(end-start));
                start++;
            }
        }
        return rectangle;

    }
}

```

## 三数之和

给你一个整数数组 nums ，判断是否存在三元组 [nums[i], nums[j], nums[k]] 满足 i != j、i != k 且 j != k ，同时还满足 nums[i] + nums[j] + nums[k] == 0 。请

你返回所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/3sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

![image-20221230123127008](D:\project\blogImage\image-20221230123127008.png)

```
    public static void main(String[] args) {
        System.out.println(threeSum(new int[]{-1, 0, 1, 2, -1, -4}));
    }

```

```
    public static List<List<Integer>> threeSum(int[] nums) {

        List<List<Integer>> list = new ArrayList<>();

        // 获取数组的长度
        int len = nums.length;
        // 如果数组为null或者小于等于3那么直接返回空列表
        if (nums==null || len<3) return list;
        // 从小到大排序
        Arrays.sort(nums);
        System.out.println(Arrays.toString(nums));
        // 遍历数组中的每一个元素
        for (int i = 0; i < len; i++) {
            // 如果起始值大于0那么直接停止循环，因为大于0那么三数相加也是大于0，不符合题目
            if (nums[i]>0){
                break;
            }
            // 如果起始值等于前一个值那么直接跳过这次循环，因为他们相加和前一次都相同都一样
            if(i>0&&nums[i]==nums[i-1]) continue;
            int j = i+1;
            int k = len-1;
            //如果j=k那么就停止循环，j<k循环相加
            while (j<k){
                int sum = nums[i]+nums[j]+nums[k];
                System.out.println("nums["+i+"] +"+" nums["+j+"] + "+" nums["+k+"] ="+(nums[i]+nums[j]+nums[k]));
                // 判断相加值是否等于0
                if (sum==0){
                    // 如果等于0就添加刀数组里面
                    list.add(Arrays.asList(nums[i],nums[j],nums[k]));
                    while (j<k&&nums[j]==nums[j+1]) j++;
                    while (j<k&&nums[k]==nums[k-1]) k--;
                    j++;
                    k--;
                    //如果sum值小于0左指针++
                } else if (sum<0) {
                    j++;
                    //如果sum值大于0右指针--
                }else if (sum>0){
                    k--;
                }

            }

        }
        return list;
    }
```

最接近的三数之和

给你一个长度为 n 的整数数组 nums 和 一个目标值 target。请你从 nums 中选出三个整数，使它们的和与 target 最接近。

返回这三个数的和。

假定每组输入只存在恰好一个解。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/3sum-closest
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

![image-20221230140958281](D:\project\blogImage\image-20221230140958281.png)

```

            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r];
                // 如果sum的值等于target则直接返回sum
                if (sum == target) return sum;
                // 如果sum值大于target，那么r--，因为上面从小到大排序，起始值+（起始值+1）+r的值都是大于target所以直接r--
                if (sum > target) {
                    if ((sum - target) < cha) {
                        res = sum;
                        cha = sum - target;
                    }
                    // nums[r] == nums[r - 1] 其实相加都一样直接在--
                    while (l < r && nums[r] == nums[r - 1]) r--;
                    r--;
                } else {
                    if ((target - sum) < cha) {
                        res = sum;
                        cha = target - sum;
                    }
                    while (l < r && nums[l] == nums[l + 1]) l++;
                    l++;
                }
            }
        }
        return res;
    }
```

