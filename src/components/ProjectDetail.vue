<template>
  <div class="project-detail">
    <button @click="goBack" class="back-button">
      ← Terug naar Projecten
    </button>

    <div class="project-header">
      <img :src="project.headerImage" :alt="project.title" class="header-image" />
      <div class="header-overlay">
        <div class="header-content">
          <div class="header-badges">
            <span class="category-badge" :class="`badge-${project.category}`">
              {{ project.category }}
            </span>
            <span v-if="project.status === 'in-progress'" class="status-badge">
              🔨 In Progress
            </span>
          </div>
          <h1 class="project-title">{{ project.title }}</h1>
        </div>
      </div>
    </div>

    <div class="project-content">
      <div class="content-section">
        <h2 class="section-title">Overzicht</h2>
        <p class="project-description">{{ project.description }}</p>
      </div>

      <div class="content-section">
        <h2 class="section-title">Over Dit Project</h2>
        <div class="project-text">
          <p v-for="(paragraph, index) in contentParagraphs" :key="index">
            {{ paragraph }}
          </p>
        </div>
      </div>

      <div class="content-section">
        <h2 class="section-title">Gebruikte vaardigheden</h2>
        <div class="tech-tags">
          <span v-for="tag in project.tags" :key="tag" class="tech-tag">
            {{ tag }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'

export default {
  name: 'ProjectDetail',
  props: {
    project: {
      type: Object,
      required: true
    }
  },
  emits: ['back'],
  setup(props, { emit }) {
    const contentParagraphs = computed(() => {
      return props.project.content ? props.project.content.split('\n\n') : []
    })

    const goBack = () => {
      emit('back')
    }

    return {
      contentParagraphs,
      goBack
    }
  }
}
</script>

<style scoped>
.project-detail {
  max-width: 900px;
  margin: 0 auto;
  animation: fadeIn 0.4s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.back-button {
  background: var(--card-bg);
  border: none;
  color: var(--text-primary);
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 500;
  margin-bottom: 1.5rem;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.back-button:hover {
  transform: translateX(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.project-header {
  position: relative;
  width: 100%;
  height: 400px;
  border-radius: 12px;
  overflow: hidden;
  margin-bottom: 2rem;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
}

.header-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.header-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  padding: 2rem;
}

.header-content {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.header-badges {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.category-badge {
  display: inline-block;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.status-badge {
  display: inline-block;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  background: #10b981;
  color: white;
}

.badge-personal {
  background: #3b82f6;
  color: white;
}

.badge-school {
  background: #10b981;
  color: white;
}

.badge-future {
  background: #8b5cf6;
  color: white;
}

.project-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: white;
  margin: 0;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.project-content {
  background: var(--card-bg);
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.content-section {
  margin-bottom: 2.5rem;
}

.content-section:last-child {
  margin-bottom: 0;
}

.section-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 2px solid #3b82f6;
}

.project-description {
  font-size: 1.1rem;
  line-height: 1.7;
  color: var(--text-secondary);
}

.project-text p {
  font-size: 1rem;
  line-height: 1.8;
  color: var(--text-secondary);
  margin-bottom: 1rem;
}

.project-text p:last-child {
  margin-bottom: 0;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.tech-tag {
  background: #3b82f6;
  color: white;
  padding: 0.6rem 1.2rem;
  border-radius: 20px;
  font-size: 0.95rem;
  font-weight: 500;
}

@media (max-width: 768px) {
  .project-header {
    height: 300px;
  }

  .project-title {
    font-size: 1.75rem;
  }

  .header-overlay {
    padding: 1.5rem;
  }

  .project-content {
    padding: 1.5rem;
  }

  .section-title {
    font-size: 1.3rem;
  }
}
</style>
