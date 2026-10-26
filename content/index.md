---
title: 金正 · AI 投研工程开发
kind: home
summary: 金正的 AI 投研工程开发：研报检索、需求拆解和上线闸门，每一步不偷看未来，每个结论都要过评审。
---

<section class="hero" aria-labelledby="hero-title">
<div class="hero-copy">
<h1 id="hero-title" class="display">AI 投研工具，<br>先证明自己<span class="surprise">没偷看未来</span>。</h1>
<p class="lead">研究员提一句需求，系统把它拆成研究计划，在当时已经入库的研报里取证、跑回测，最后按事先写定的 12 项标准出一张上线评审单。拿我自己的指增、文本因子和行业景气来试：信息比最高的那一版，正是闸门否掉的那一版。</p>
</div>
<div class="hero-side">
<div class="actions"><a class="btn primary" href="gate/">看上线闸门</a><a class="btn" href="mailto:zheng.jin20@student.xjtlu.edu.cn">发邮件</a></div>
</div>
<figure class="hero-figure">
{{svg:flow}}
<figcaption>从一句需求到上线评审。模型只负责拆计划和成文；取证、回测、评审都是固定流程，时点规则在每一步由代码执行。</figcaption>
</figure>
</section>

<section class="band">
<div class="ruler" aria-hidden="true"></div>
<div class="band-head"><h2>研究问题</h2></div>
<div class="thesis">
<div>
<p>大模型做投研，最危险的不是答不上来，而是三件看起来没问题的事：检索到了当时还没发出来的研报；模型凭记忆说出了它不该知道的结果；回测从十几个版本里挑了最好看的那个。这三件事都会让回测更漂亮，上线以后却不成立。</p>
<p>所以我把投研流程拆成可以检验的几步，每一步都量化它有没有偷看未来、结论能不能复现，再用一道事先写定标准的闸门，决定一条研究结论能不能上线。</p>
</div>
<div>
<dl class="facts">
<div class="fact"><dt>研报</dt><dd>57,143 篇券商研报摘要，切成 19 万个片段，每段都带入库时刻</dd></div>
<div class="fact"><dt>闸门</dt><dd>12 项检查，阈值在看结果之前写定；审计了 20 个候选</dd></div>
<div class="fact"><dt>评测</dt><dd>64 道检索问答题，30 道需求拆解题，每个选择都按事先写定的规则定</dd></div>
<div class="fact"><dt>花费</dt><dd>全部大模型调用合计 0.58 美元</dd></div>
</dl>
</div>
</div>
</section>

<section class="band">
<div class="ruler" aria-hidden="true"></div>
<div class="band-head"><h2>三个发现</h2></div>
<div class="findings">
<div class="finding">
<h3>检索不偷看未来</h3>
{{svg:mini-retrieval}}
<p>研报按东财的入库时刻（精确到秒）才能被检索到，过滤放在打分之前。64 道按研报出的题、768 次检索，没有一次返回查询时点之后的研报；向量加关键词的混合召回最好，MRR 0.74。</p>
<a class="more" href="rag/">在检索问答里看</a>
</div>
<div class="finding">
<h3>把规则写进提示词，比换模型管用</h3>
{{svg:mini-ab}}
<p>30 条模糊需求、每条跑 3 次：把今天的日期、时点换算规则和候选清单写进提示词，研究计划完全正确的比例从 40% 升到 93%（McNemar p = 0.0004）。换更贵的模型只多 10 个点、不显著，按规则留用便宜的。</p>
<a class="more" href="planner/">在需求拆解里看</a>
</div>
<div class="finding">
<h3>闸门否掉了最好看的那版</h3>
{{svg:mini-gate}}
<p>加了 Qwen 3.7 文本因子的中证500 指增信息比最高，但模型知识截止日之后只有 5 周回测，排除不了它记得未来，判不通过。大模型读研报摘要做的行业景气年化超额 7.7%，超额都在模型截止日之后，可 t 值只有 1.72，只够放进观察池。</p>
<a class="more" href="gate/">在上线闸门里看</a>
</div>
</div>
</section>

<section class="band">
<div class="ruler" aria-hidden="true"></div>
<div class="band-head"><h2>三部分</h2></div>
<ul class="rows">
<li><span class="date">检索问答</span><div><a class="t" href="rag/">研报检索与问答：只用当时已入库的研报</a><p>向量加关键词混合召回，检索前按入库时刻过滤；回答逐句标出处、代码核对数字，时点陷阱下没有说漏一个未来的数字。</p></div></li>
<li><span class="date">需求拆解</span><div><a class="t" href="planner/">需求拆解与 MCP 工具：模型只负责拆计划</a><p>研究计划用 JSON Schema 描述、按数据字典校验，执行走固定流程；7 个 MCP 工具；提示词和模型都用 A/B 测试来选。</p></div></li>
<li><span class="date">上线闸门</span><div><a class="t" href="gate/">上线闸门：12 项检查，阈值事先写定</a><p>显著性、紧缩夏普、过拟合概率、成本、安慰剂、大模型知识截止日、风控阈值和回测审计；20 个候选里没有一个直接通过。</p></div></li>
</ul>
</section>

<section class="band">
<div class="ruler" aria-hidden="true"></div>
<div class="band-head"><h2>关于这个项目</h2><a href="about/">数据与局限</a></div>
<dl class="facts">
<div class="fact"><dt>数据</dt><dd>东方财富研报中心公开页面上的个股研报摘要（2021 年 7 月起，沪深300、中证500 历史成分股）</dd><dd>行情和申万行业来自本地行情库；研报原文不转载，只放统计结果和出处</dd></div>
<div class="fact"><dt>模型</dt><dd>检索用本地 BGE-M3；Llama 3.1 8B 读摘要打标签，qwen3.7 / qwen3.8 拆计划和作答</dd></div>
<div class="fact"><dt>工程</dt><dd>Python；MCP 服务 7 个工具；40 个离线测试；每次模型调用记账，有预算保险丝</dd></div>
<div class="fact"><dt>作者</dt><dd>金正，金融计算硕士在读；宏观利率研究见 <a href="https://joyzen2.github.io/">宏观研究站</a></dd></div>
</dl>
</section>
