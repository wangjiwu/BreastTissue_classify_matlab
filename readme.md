<div id="content_views" class="markdown_views prism-atom-one-dark">
							<!-- flowchart 箭头图标 勿删 -->
							<svg xmlns="http://www.w3.org/2000/svg" style="display: none;"><path stroke-linecap="round" d="M5,0 0,2.5 5,5z" id="raphael-marker-block" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></path></svg>
							<h1><a name="t0"></a><a id="_0" target="_blank"></a>前言</h1>
<p>此教程专注于<strong>刚入门的小白</strong>， 且博客拥有<strong>时效性</strong>， 发布于2019年3月份， 可能后面的读者会发现一些问题， 欢迎底下评论出现的问题，我将尽可能更新解决方案。</p>
<p>我开始也在如何安装libsvm上出现了很多问题， 而网上的解决方案大都有一些问题，且发布时间比较早， 方案已经过时，于是我把经历的坑总结起来，供大家学习</p>
<h1><a name="t1"></a><a id="_6" target="_blank"></a>版本声明</h1>
<p><strong>我的matlab版本为2016a， win10系统， 安装的是最新版的libsvm， version3.2.3</strong></p>
<h1><a name="t2"></a><a id="libsvm_9" target="_blank"></a>一，配置libsvm</h1>
<h2><a name="t3"></a><a id="1libsvm_11" target="_blank"></a>1.首先需要下载libsvm包：</h2>
<p><a href="http://www.csie.ntu.edu.tw/~cjlin/libsvm/" rel="nofollow" target="_blank">http://www.csie.ntu.edu.tw/~cjlin/libsvm/</a></p>
<h2><a name="t4"></a><a id="2libsvm323matlabtoolbox_14" target="_blank"></a>2.将libsvm3.2.3解压到matlab/toolbox目录下：</h2>
<p>若不知道路径在哪， 可以点击设置路径来找到</p>
<p><img src="https://img-blog.csdnimg.cn/20190324201208795.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxODc0NDU1OTUz,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"></p>
<h2><a name="t5"></a><a id="3_libsvm323__18" target="_blank"></a>3. 在设置路径里把刚才加入的libsvm3.2.3 加入到路径</h2>
<p><strong>注意matlab和windows这两个文件夹都要加入 否则将会出错</strong></p>
<p><img src="https://img-blog.csdnimg.cn/20190324201411693.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxODc0NDU1OTUz,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"></p>
<h2><a name="t6"></a><a id="4libsvm_323matlab__23" target="_blank"></a>4.将当前路径设置到libsvm 3.2.3/matlab 后，在命令行窗口运行</h2>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">mex -setup
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre>
<p>若已经安装c++编译环境则会出现下面的情况，  （我已经安装过VS 2017了） <strong>若提示没有c++编译环境则需要自己安装环境了，</strong><br>
<img src="https://img-blog.csdnimg.cn/20190324201738734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxODc0NDU1OTUz,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"><br>
<strong>直接点击用c++编译</strong><br>
<img src="https://img-blog.csdnimg.cn/20190324202257966.png" alt="在这里插入图片描述"></p>
<h2><a name="t7"></a><a id="5__34" target="_blank"></a>5. 源码编译</h2>
<p>打开当前目录下的make.m文件<br>
<img src="https://img-blog.csdnimg.cn/20190324202502455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxODc0NDU1OTUz,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"><br>
将其中所的<strong>CFLAGS替换为COMPFLAGS</strong>（替换运用CTRL+F即可），替换后执行make则可以编译成功。（这里我已经改完了， 一般没改的话 都是CFLAGS） <strong>这里也就是以前教程忽略的一点，没有这一步将出现编译失败</strong></p>
<p>编译完之后可以得到多出的这四个<strong>后缀为mexw64文件</strong>， 这说明我们已经完成安装了<br>
<img src="https://img-blog.csdnimg.cn/20190324202744484.png" alt="在这里插入图片描述"></p>
<h1><a name="t8"></a><a id="_libsvm_41" target="_blank"></a>二， 使用libsvm进行分类</h1>
<p>首先给出实例地址 方便下载 <a href="https://github.com/wangjiwu/BreastTissue_classify_matlab" rel="nofollow" target="_blank">https://github.com/wangjiwu/BreastTissue_classify_matlab</a></p>
<p>这里给出了101个数据， 每一个数据都有9个特征和一个分类标签</p>
<p><img src="https://img-blog.csdnimg.cn/20190324210014692.png" alt="在这里插入图片描述"><br>
用这些数据来生成测试集和训练集， 得到模型并且测试，分类</p>
<h2><a name="t9"></a><a id="_52" target="_blank"></a>代码流程</h2>
<div><ul><li><a href="#1" rel="nofollow" target="_self">I. 清空环境变量</a></li><li><a href="#2" rel="nofollow" target="_self">II. 导入数据</a></li><li><a href="#6" rel="nofollow" target="_self">III. 数据归一化</a></li><li><a href="#7" rel="nofollow" target="_self">IV. SVM创建/训练(RBF核函数)</a></li><li><a href="#10" rel="nofollow" target="_self">V. SVM仿真测试</a></li><li><a href="#11" rel="nofollow" target="_self">VI. 绘图</a></li></ul></div>
<h3><a name="t10"></a><a id="I__56" target="_blank"></a>I. 清空环境变量</h3>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">clear all
clc
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li></ul></pre>
<h3><a name="t11"></a><a id="II__62" target="_blank"></a>II. 导入数据</h3>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">load BreastTissue_data.mat
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre>
<ol>
<li>随机产生训练集和测试集</li>
</ol>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">n = randperm(size(matrix,1));
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre>
<ol start="2">
<li>训练集——80个样本</li>
</ol>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">train_matrix = matrix(n(1:80),:);
train_label = label(n(1:80),:);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li></ul></pre>
<ol start="3">
<li>测试集——26个样本</li>
</ol>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">test_matrix = matrix(n(81:end),:);
test_label = label(n(81:end),:);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li></ul></pre>
<h3><a name="t12"></a><a id="III__80" target="_blank"></a>III. 数据归一化</h3>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">
%% III. 数据归一化
[Train_matrix,PS] = mapminmax(train_matrix');
Train_matrix = Train_matrix';
Test_matrix = mapminmax('apply',test_matrix',PS);
Test_matrix = Test_matrix';
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li></ul></pre>
<h3><a name="t13"></a><a id="IV_SVMRBF_91" target="_blank"></a>IV. SVM创建/训练(RBF核函数)</h3>
<p><strong>这里使用的是交叉验证的方法 选出等距的多种c和g训练找到最合适的c和g，如果训练时间较长可以直接输入参数，跳过这一步</strong></p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">cmd = ' -t 2 -c 42.2243 -g 2.639' 
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre>
<p>若参数不知道具体的代表意思可参考此博客<br>
<a href="https://blog.csdn.net/mrfortitude/article/details/59558037" rel="nofollow" target="_blank">https://blog.csdn.net/mrfortitude/article/details/59558037</a></p>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">[c,g] = meshgrid(-10:0.2:10,-10:0.2:10);
[m,n] = size(c);
cg = zeros(m,n);
eps = 10^(-4);
v = 5;
bestc = 1;
bestg = 0.1;
bestacc = 0;
for i = 1:m
    for j = 1:n
        cmd = ['-v ',num2str(v),' -t 2',' -c ',num2str(2^c(i,j)),' -g ',num2str(2^g(i,j))];
        cg(i,j) = svmtrain(train_label,Train_matrix,cmd);
        if cg(i,j) &gt; bestacc
            bestacc = cg(i,j);
            bestc = 2^c(i,j);
            bestg = 2^g(i,j);
        end
        if abs( cg(i,j)-bestacc )&lt;=eps &amp;&amp; bestc &gt; 2^c(i,j)
            bestacc = cg(i,j);
            bestc = 2^c(i,j);
            bestg = 2^g(i,j);
        end
    end
end
cmd = [' -t 2',' -c ',num2str(bestc),' -g ',num2str(bestg)];
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li><li style="color: rgb(153, 153, 153);">7</li><li style="color: rgb(153, 153, 153);">8</li><li style="color: rgb(153, 153, 153);">9</li><li style="color: rgb(153, 153, 153);">10</li><li style="color: rgb(153, 153, 153);">11</li><li style="color: rgb(153, 153, 153);">12</li><li style="color: rgb(153, 153, 153);">13</li><li style="color: rgb(153, 153, 153);">14</li><li style="color: rgb(153, 153, 153);">15</li><li style="color: rgb(153, 153, 153);">16</li><li style="color: rgb(153, 153, 153);">17</li><li style="color: rgb(153, 153, 153);">18</li><li style="color: rgb(153, 153, 153);">19</li><li style="color: rgb(153, 153, 153);">20</li><li style="color: rgb(153, 153, 153);">21</li><li style="color: rgb(153, 153, 153);">22</li><li style="color: rgb(153, 153, 153);">23</li><li style="color: rgb(153, 153, 153);">24</li><li style="color: rgb(153, 153, 153);">25</li></ul></pre>
<p>创建/训练SVM模型</p>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">model = svmtrain(train_label,Train_matrix,cmd);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre>
<h3><a name="t14"></a><a id="V_SVM_132" target="_blank"></a>V. SVM仿真测试</h3>
<p>注意一定要 传入3个参数而不是两个， 且 <strong>测试lable 是m<em>1的矩阵， 测试矩阵是m</em>n的矩阵</strong>   m为样本个数， n为特征个数</p>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">[predict_label_1,accuracy_1,prob_estimates] = svmpredict(train_label,Train_matrix,model);
[predict_label_2,accuracy_2,prob_estimates2] = svmpredict(test_label,Test_matrix,model);
result_1 = [train_label predict_label_1];
result_2 = [test_label predict_label_2];
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li></ul></pre>
<p>结果如下<br>
<img src="https://img-blog.csdnimg.cn/20190324205224344.png" alt="在这里插入图片描述"></p>
<h3><a name="t15"></a><a id="VI__144" target="_blank"></a>VI. 绘图</h3>
<pre class="prettyprint"><code class="prism language-matlab has-numbering" onclick="mdcp.copyCode(event)">figure
plot(1:length(test_label),test_label,'r-*')
hold on
plot(1:length(test_label),predict_label_2,'b:o')
grid on
legend('真实类别','预测类别')
xlabel('测试集样本编号')
ylabel('测试集样本类别')
string = {'测试集SVM预测结果对比(RBF核函数)';
          ['accuracy = ' num2str(accuracy_2(1)) '%']};
title(string)
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li><li style="color: rgb(153, 153, 153);">7</li><li style="color: rgb(153, 153, 153);">8</li><li style="color: rgb(153, 153, 153);">9</li><li style="color: rgb(153, 153, 153);">10</li><li style="color: rgb(153, 153, 153);">11</li></ul></pre>
<p><img src="https://img-blog.csdnimg.cn/20190324205136186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxODc0NDU1OTUz,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"></p>

            </div>
