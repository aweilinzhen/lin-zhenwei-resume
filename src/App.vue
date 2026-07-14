<script setup>
import { ref } from 'vue'
import { resume } from './data/resume'

const copied = ref(false)

const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText(resume.profile.email)
    copied.value = true
    window.setTimeout(() => (copied.value = false), 1800)
  } catch {
    window.location.href = `mailto:${resume.profile.email}`
  }
}

const printResume = () => window.print()
</script>

<template>
  <div class="site-shell">
    <header class="topbar">
      <a class="brand" href="#top" aria-label="返回顶部">
        <span class="brand-mark">LZ</span>
        <span>{{ resume.profile.name }}</span>
      </a>
      <nav class="nav" aria-label="页面导航">
        <a href="#research">AI 项目</a>
        <a href="#experience">工作经历</a>
        <a href="#education">教育背景</a>
      </nav>
      <button class="ghost-btn desktop-action" type="button" @click="printResume">打印 / 保存 PDF</button>
    </header>

    <main id="top">
      <section class="hero section-wrap">
        <div class="hero-copy">
          <p class="eyebrow">{{ resume.profile.englishName }} · PRODUCT PORTFOLIO</p>
          <h1>
            把复杂的企业流程，<br />
            设计成<span>可执行的产品能力。</span>
          </h1>
          <p class="hero-role">{{ resume.profile.title }}</p>
          <div class="tag-row">
            <span v-for="tag in resume.profile.tags" :key="tag">{{ tag }}</span>
          </div>
          <p class="hero-summary">{{ resume.profile.summary }}</p>
          <div class="hero-actions">
            <a class="primary-btn" href="#research">查看代表项目</a>
            <button class="secondary-btn" type="button" @click="printResume">打印 / 保存 PDF</button>
          </div>
        </div>

        <aside class="profile-card">
          <div>
            <p class="card-kicker">当前求职方向</p>
            <h2>企业 AI / AI Workflow / AI Agent 产品经理</h2>
          </div>
          <dl>
            <div>
              <dt>所在地意向</dt>
              <dd>{{ resume.profile.location }}</dd>
            </div>
            <div>
              <dt>电话</dt>
              <dd><a :href="`tel:${resume.profile.phone}`">{{ resume.profile.phone }}</a></dd>
            </div>
            <div>
              <dt>邮箱</dt>
              <dd><button class="text-button" type="button" @click="copyEmail">{{ copied ? '已复制邮箱' : resume.profile.email }}</button></dd>
            </div>
          </dl>
          <div class="profile-note">产品背景 × 技术理解 × 企业流程自动化</div>
        </aside>
      </section>

      <section class="stats section-wrap" aria-label="核心数据">
        <div v-for="item in resume.highlights" :key="item.label" class="stat-item">
          <strong>{{ item.value }}</strong>
          <span>{{ item.label }}</span>
        </div>
      </section>

      <section class="section-wrap two-column-section">
        <div class="section-heading sticky-heading">
          <p class="section-index">01</p>
          <h2>能力结构</h2>
          <p>兼具企业平台产品经验、业务流程抽象能力与 LLM 应用实践。</p>
        </div>
        <div class="capability-grid">
          <article v-for="item in resume.capabilities" :key="item.name" class="capability-card">
            <h3>{{ item.name }}</h3>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section id="research" class="section-wrap two-column-section research-section">
        <div class="section-heading sticky-heading">
          <p class="section-index">02</p>
          <h2>AI 研究项目</h2>
          <p>不是概念 Demo，而是一条从自然语言理解到工作流执行验证的完整链路。</p>
        </div>
        <article class="research-card">
          <div class="research-topline">
            <span>FEATURED PROJECT</span>
            <span>{{ resume.research.meta }}</span>
          </div>
          <h3>{{ resume.research.title }}</h3>
          <p class="research-description">{{ resume.research.description }}</p>
          <ul class="detail-list">
            <li v-for="item in resume.research.bullets" :key="item">{{ item }}</li>
          </ul>
          <div class="stack-list">
            <span v-for="item in resume.research.stack" :key="item">{{ item }}</span>
          </div>
        </article>
      </section>

      <section id="experience" class="section-wrap two-column-section">
        <div class="section-heading sticky-heading">
          <p class="section-index">03</p>
          <h2>工作经历</h2>
          <p>持续深耕 PaaS、低代码、工作流和企业数字化产品。</p>
        </div>
        <div class="timeline">
          <article v-for="item in resume.experiences" :key="item.company" class="timeline-item">
            <div class="timeline-marker"></div>
            <div class="experience-header">
              <div>
                <h3>{{ item.company }}</h3>
                <p>{{ item.role }}</p>
              </div>
              <time>{{ item.period }}</time>
            </div>
            <p class="experience-intro">{{ item.intro }}</p>
            <ul class="detail-list compact-list">
              <li v-for="bullet in item.bullets" :key="bullet">{{ bullet }}</li>
            </ul>
          </article>
        </div>
      </section>

      <section class="section-wrap two-column-section">
        <div class="section-heading sticky-heading">
          <p class="section-index">04</p>
          <h2>代表产品</h2>
          <p>从平台底层能力到商业化结果，强调可复用和可交付。</p>
        </div>
        <div class="product-grid">
          <article v-for="item in resume.products" :key="item.title" class="product-card">
            <p class="product-period">{{ item.period }}</p>
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section id="education" class="section-wrap two-column-section final-section">
        <div class="section-heading sticky-heading">
          <p class="section-index">05</p>
          <h2>教育与成果</h2>
          <p>持续把过往平台经验迁移到人工智能与企业自动化场景。</p>
        </div>
        <div class="education-content">
          <div class="education-list">
            <article v-for="item in resume.education" :key="item.school" class="education-item">
              <div>
                <h3>{{ item.school }}</h3>
                <p>{{ item.degree }}</p>
              </div>
              <time>{{ item.period }}</time>
              <p class="education-detail">{{ item.detail }}</p>
            </article>
          </div>
          <div class="achievement-panel">
            <h3>专利与认可</h3>
            <ul class="detail-list compact-list">
              <li v-for="item in resume.achievements" :key="item">{{ item }}</li>
            </ul>
          </div>
        </div>
      </section>

      <section class="contact-section">
        <div class="section-wrap contact-inner">
          <div>
            <p class="eyebrow">LET'S BUILD BETTER WORKFLOWS</p>
            <h2>期待参与企业 AI 与复杂流程产品的建设。</h2>
          </div>
          <div class="contact-actions">
            <a class="primary-btn light" :href="`mailto:${resume.profile.email}`">发送邮件</a>
            <button class="secondary-btn dark" type="button" @click="copyEmail">{{ copied ? '邮箱已复制' : '复制邮箱' }}</button>
          </div>
        </div>
      </section>
    </main>

    <footer class="footer section-wrap">
      <span>© 2026 {{ resume.profile.name }}</span>
      <span>Vue 3 · Vite · GitHub Pages</span>
    </footer>
  </div>
</template>
