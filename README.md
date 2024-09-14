| 这个作业属于哪个课程 | https://edu.cnblogs.com/campus/gdgy/CSGrade22-34/               |
| ---------- | --------------------------------------------------------------- |
| 这个作业要求在哪里  | https://edu.cnblogs.com/campus/gdgy/CSGrade22-34/homework/13229 |
| 这个作业的目标    | 开发个人项目，实现项目单元测试                                                 |
| 个人github仓库地址     |   https://github.com/Atigul/3222004973/tree/main   |

文章目录
0、 前言
  0.1、需求
    0.2、 要求
      0.3、 开发环境
1.0、 整体设计
  1.1、 整体流程
2.0、 性能分析****
3.0、单元测试
    3.1、 主程序main的测试
4.0、 PSP表格
****0、 前言****
**0.1、需求**
**题目：论文查重**
描述如下：
设计一个论文查重算法，给出一个原文文件和一个在这份原文上经过了增删改的抄袭版论文的文件，在答案文件中输出其重复率。

原文示例：今天是星期天，天气晴，今天晚上我要去看电影。
抄袭版示例：今天是周天，天气晴朗，我晚上要去看电影。
要求输入输出采用文件输入输出，规范如下：
********
从命令行参数给出：论文原文的文件的绝对路径。
从命令行参数给出：抄袭版论文的文件的绝对路径。
从命令行参数给出：输出的答案文件的绝对路径。
**0.2、 要求**
1.在Gitcode仓库中新建一个学号为名的文件夹。
2.在开始实现程序之前，在PSP表格记录下你估计在程序开发各个步骤上耗费的时间，在你实现程序之后，在PSP表格记录下你在程序的各个模块上实际花费的时间。
3.使用C++ 、Java语言或者python3实现，提交python代码时请附带上requirements.txt，。C++请使用Visual Studio Community 2017进行开发，运行环境为64-bit Windows 10。对于C++/Java，还需将编译好的程序发布到Gitcode仓库中的releases中
4.提交的代码要求经过Code Quality Analysis工具的分析并消除所有的警告。
5.完成项目的首个版本之后，请使用性能分析工具Studio Profiling Tools来找出代码中的性能瓶颈并进行改进。
6.使用Gitcode来管理源代码和测试用例，代码有进展即签入Gitcode。签入记录不合理的项目会被助教抽查询问项目细节。
7.使用单元测试对项目进行测试，并使用插件查看测试分支覆盖率等指标；写出至少10个测试用例确保你的程序能够正确处理各种情况。
**0.3、 开发环境**
编译语言：Java 17
IDE：Intellij IDEA 2021.3.2
项目构建工具：maven
单元测试：JUnit 4.12
性能分析工具：JProfiler 9.2
依赖的外部 jar 包：汉语言处理包
****1.0、 整体设计****
**1.1、 整体流程**
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914185702936-300707638.png)
**2.0、 性能分析******
总览
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914190354932-1896436388.png)
方法调用次数
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914190859220-25654211.png)
从这里可以看出首先最多调用的是int数组，因为SimHash算法的底层需要调用大量的int数组作为容器分装文章的句子，其次调用的就是hankcs包中的工具类，主要都是用于SimHash算法的分词和计算调用的总结：暂时没有想到什么改进方法
**3.0、单元测试**
测试方法如下：
测试输入正确方法参数和输入错误方法参数
3.1 主程序main的测试
public class mainTest {
    @Test
    void test1() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }

    @Test
    void test2() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig_0.8_add.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }

    @Test
    void test3() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig_0.8_del.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }

    @Test
    void test4() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig_0.8_dis_1.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }

    @Test
    void test5() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig_0.8_dis_10.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }

    @Test
    void test6() throws IOException {
        ReadFile rf=new ReadFile();
        String article1=rf.read("D:\\working\\gdut-s\\3222004973\\orig.txt");
        String article2=rf.read("D:\\working\\gdut-s\\3222004973\\orig_0.8_dis_15.txt");

        long l3 = System.currentTimeMillis();
        SimHash hash1 = new SimHash(article1, 64);
        SimHash hash2 = new SimHash(article2, 64);
        System.out.println("======================================");
        System.out.println("海明距离：" + hash1.hammingDistance(hash2));
        System.out.println("文本相似度：" + hash1.getSemblance(hash2));
        long l4 = System.currentTimeMillis();
        System.out.println(l4 - l3);
        System.out.println("======================================");
    }
}
测试结果：
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914191534800-354149203.png)
代码覆盖率：
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914191813130-63613032.png)
结果反馈：
![](https://img2024.cnblogs.com/blog/3512873/202409/3512873-20240914192630753-1125487991.png)
**4.0、 PSP表格**
PSP是卡耐基梅隆大学（CMU）的专家们针对软件工程师所提出的一套模型：Personal Software Process (PSP， 个人开发流程，或称个体软件过程)。
| PSP2.1                                | Personal Software Process Stages | 预估耗时（分钟） | 实际耗时（分钟） |
| ------------------------------------- | -------------------------------- | -------- | -------- |
| Planning                              | 计划                               | 60     |  40        |
| Estimate                              | 估计这个任务需要多少时间                     | 20       | 20       |
| Development                           | 开发                               | 1290     | 1425     |
| Analysis                              | 需求分析 (包括学习新技术)                   | 360    | 480     |
| Design Spec                           | 生成设计文档                           | 60    | 80     |
| Design Review                         | 设计复审                             | 30      | 25     |
| Coding Standard                       | 代码规范 (为目前的开发制定合适的规范)             | 30      | 30    |
| Design                                | 具体设计                             | 90    | 90      |
| Coding                                | 具体编码                             | 360     | 420     |
| Code Review                           | 代码复审                             | 60    | 60     |
| Test                                  | 测试（自我测试，修改代码，提交修改）               | 300      | 240       |
| Reporting                             | 报告                               | 60    | 60     |
| Test Repor                            | 测试报告                             | 60       | 30       |
| Size Measurement                      | 计算工作量                            | 30      | 30       |
| Postmortem & Process Improvement Plan | 事后总结, 并提出过程改进计划                  | 90       | 60       |
| 合计                                    |                                  | 1620    | 1665    |
