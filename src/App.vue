<script setup>
import { ref } from 'vue'
import { resume } from './data/resume'

const copied = ref(false)

const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText(resume.profile.email)
    copied.value = true
    window.setTimeout(() => (copied.value = false), 1600)
  } catch {
    window.location.href = `mailto:${resume.profile.email}`
  }
}

const printResume = () => window.print()
</script>

<template>
  <div class="resume-page">
    <header class="resume-header">
      <div class="identity">
        <p class="english-name">{{ resume.profile.englishName }}</p>
        <h1>{{ resume.profile.name }}</h1>
        <p class="role">{{ resume.profile.title }} · 企业 AI / AI Workflow / 低代码平台</p>
        <p class="summary">{{ resume.profile.summary }}</p>

        <div class="contact-row" aria-label="联系方式">
          <a :href="`tel:${resume.profile.phone}`">{{ resume.profile.phone }}</a>
          <button type="button" @click="copyEmail">
            {{ copied ? '邮箱已复制' : resume.profile.email }}
          </button>
          <span>{{ resume.profile.location }}</span>
        </div>
      </div>

      <button class="print-button" type="button" @click="printResume">打印 / 保存 PDF</button>
    </header>

    <main>
      <section class="resume-section">
        <h2>核心能力</h2>
        <div class="skills-grid">
          <article v-for="item in resume.capabilities" :key="item.name" class="skill-item">
            <h3>{{ item.name }}</h3>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section class="resume-section" id="research">
        <div class="section-title-row">
          <h2>代表项目</h2>
          <span>{{ resume.research.meta }}</span>
        </div>

        <article class="featured-project">
          <h3>{{ resume.research.title }}</h3>
          <p class="project-summary">{{ resume.research.description }}</p>
          <ul class="bullet-list">
            <li v-for="item in resume.research.bullets" :key="item">{{ item }}</li>
          </ul>
          <p class="tech-stack">{{ resume.research.stack.join(' · ') }}</p>
        </article>
      </section>

      <section class="resume-section" id="experience">
        <h2>工作经历</h2>

        <div class="experience-list">
          <article v-for="item in resume.experiences" :key="item.company" class="experience-item">
            <div class="experience-title">
              <div>
                <h3>{{ item.company }}</h3>
                <p>{{ item.role }}</p>
              </div>
              <time>{{ item.period }}</time>
            </div>

            <p class="experience-intro">{{ item.intro }}</p>
            <ul class="bullet-list compact">
              <li v-for="bullet in item.bullets" :key="bullet">{{ bullet }}</li>
            </ul>
          </article>
        </div>
      </section>

      <section class="resume-section">
        <h2>代表产品</h2>
        <div class="product-list">
          <article v-for="item in resume.products" :key="item.title" class="product-item">
            <div class="product-heading">
              <h3>{{ item.title }}</h3>
              <span>{{ item.period }}</span>
            </div>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section class="resume-section" id="education">
        <h2>教育背景</h2>
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
      </section>

      <section class="resume-section achievements-section">
        <h2>专利与认可</h2>
        <ul class="bullet-list two-columns">
          <li v-for="item in resume.achievements" :key="item">{{ item }}</li>
        </ul>
      </section>
    </main>

    <footer class="resume-footer">
      <span>© 2026 {{ resume.profile.name }}</span>
      <a :href="`mailto:${resume.profile.email}`">{{ resume.profile.email }}</a>
    </footer>
  </div>
</template>
