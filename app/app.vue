<template>
  <div class="page">
    <NuxtRouteAnnouncer />

    <header class="hero">
      <div class="hero__top">
        <p class="eyebrow">{{ copy.heroEyebrow }}</p>
        <div class="language-toggle" role="group" aria-label="Language toggle">
          <button v-for="option in languageOptions" :key="option.id" type="button"
            :class="['language-toggle__btn', { active: option.id === currentLanguage }]"
            @click="currentLanguage = option.id">
            {{ option.shortLabel }}
          </button>
        </div>
      </div>
      <div class="hero__body">
        <div class="hero__text">
          <h1 class="hero__title">Melissa Tran</h1>
          <p class="intro">
            {{ copy.heroIntro }}
          </p>
          <div class="cta">
            <a class="primary" :href="profileUrl" target="_blank" rel="noopener">
              {{ copy.ctaListings }}
            </a>
          </div>
        </div>
        <div class="hero__photo">
          <img src="/profile.jpg" alt="Portrait of Melissa Tran">
        </div>
      </div>
    </header>

    <section class="panel contact">
      <div class="panel__content">
        <h2>{{ copy.contactTitle }}</h2>
        <p>{{ copy.contactIntro }}</p>
      </div>
      <div class="contact__details">
        <div v-for="detail in contactDetails" :key="detail.label">
          <p class="meta-label">{{ detail.label }}</p>
          <a v-if="detail.href" :href="detail.href" target="_blank" rel="noopener">
            {{ detail.value }}
          </a>
          <p v-else>{{ detail.value }}</p>
        </div>
      </div>
    </section>

    <!-- <section class="panel languages">
      <div class="panel__content">
        <h2>{{ copy.languagesTitle }}</h2>
        <p>{{ copy.languagesIntro }}</p>
      </div>
      <ul class="languages__list">
        <li v-for="languageName in copy.languagesList" :key="languageName">
          {{ languageName }}
        </li>
      </ul>
    </section> -->

    <footer>
      <p>
        © {{ new Date().getFullYear() }} · {{ copy.footerNote }}
      </p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

const profileUrl =
  'https://www.realtor.ca/agent/2185016/melissa-tran-700-413-rue-saint-jacques-montreal-quebec-h2y1n9'

const languageOptions = [
  { id: 'en', label: 'English', shortLabel: 'EN' },
  { id: 'fr', label: 'Français', shortLabel: 'FR' },
  { id: 'zh-hans', label: '中文（普通话）', shortLabel: '中文' },
  { id: 'vi', label: 'Tiếng Việt', shortLabel: 'VI' },
  { id: 'zh-yue', label: '粵語', shortLabel: '粵' }
] as const

type LanguageId = (typeof languageOptions)[number]['id']

type TranslationCopy = {
  heroEyebrow: string
  heroIntro: string
  ctaEmail: string
  ctaListings: string
  languagesTitle: string
  languagesIntro: string
  languagesList: string[]
  contactTitle: string
  contactIntro: string
  contactLabels: { email: string; office: string }
  officeAddress: string
  footerNote: string
  realtorLinkLabel: string
}

const translations: Record<LanguageId, TranslationCopy> = {
  en: {
    heroEyebrow: 'Residential real estate',
    heroIntro:
      'Real estate broker based in Montréal, focused on clear communication and steady guidance for every transaction.',
    ctaEmail: 'Email Melissa',
    ctaListings: 'View current listings',
    languagesTitle: 'Languages',
    languagesIntro: 'Conversations available in:',
    languagesList: ['English', 'Français', '普通话', 'Tiếng Việt', '廣東話'],
    contactTitle: 'Contact',
    contactIntro: "Reach out when you're ready to start the conversation.",
    contactLabels: { email: 'Email', office: 'Office' },
    officeAddress: '700-413 Rue Saint-Jacques, Montréal, QC H2Y 1N9',
    footerNote: 'Licensed Real Estate Broker',
    realtorLinkLabel: 'Realtor.ca profile'
  },
  fr: {
    heroEyebrow: 'Immobilier résidentiel',
    heroIntro:
      'Courtière immobilière à Montréal, privilégiant une communication claire et un accompagnement constant.',
    ctaEmail: 'Écrire à Melissa',
    ctaListings: 'Consulter les inscriptions',
    languagesTitle: 'Langues',
    languagesIntro: 'Disponible pour des échanges en :',
    languagesList: ['Anglais', 'Français', 'Mandarin', 'Vietnamien', 'Cantonais'],
    contactTitle: 'Contact',
    contactIntro: 'Communiquez quand vous serez prêt à démarrer.',
    contactLabels: { email: 'Courriel', office: 'Bureau' },
    officeAddress: '700-413, rue Saint-Jacques, Montréal, QC H2Y 1N9',
    footerNote: 'Courtière immobilière agréée',
    realtorLinkLabel: 'Profil Realtor.ca'
  },
  'zh-hans': {
    heroEyebrow: '住宅房地产',
    heroIntro: '常驻蒙特利尔的房地产经纪，强调清晰沟通与稳健指引。',
    ctaEmail: '给 Melissa 发邮件',
    ctaListings: '查看房源',
    languagesTitle: '可用语言',
    languagesIntro: '提供以下语言的沟通：',
    languagesList: ['英语', '法语', '普通话', '越南语', '粤语'],
    contactTitle: '联系',
    contactIntro: '准备好开始洽谈时欢迎随时联系。',
    contactLabels: { email: '邮箱', office: '办公室' },
    officeAddress: '700-413 Rue Saint-Jacques, Montréal, QC H2Y 1N9',
    footerNote: '持牌房地产经纪',
    realtorLinkLabel: 'Realtor.ca 个人页'
  },
  vi: {
    heroEyebrow: 'Bất động sản dân dụng',
    heroIntro:
      'Môi giới tại Montréal, chú trọng giao tiếp rõ ràng và sự hướng dẫn vững vàng trong từng giao dịch.',
    ctaEmail: 'Gửi email cho Melissa',
    ctaListings: 'Xem danh sách hiện có',
    languagesTitle: 'Ngôn ngữ',
    languagesIntro: 'Có thể hỗ trợ bằng:',
    languagesList: ['Tiếng Anh', 'Tiếng Pháp', 'Tiếng Quan thoại', 'Tiếng Việt', 'Tiếng Quảng Đông'],
    contactTitle: 'Liên hệ',
    contactIntro: 'Hãy liên lạc khi bạn sẵn sàng bắt đầu trao đổi.',
    contactLabels: { email: 'Email', office: 'Văn phòng' },
    officeAddress: '700-413 Rue Saint-Jacques, Montréal, QC H2Y 1N9',
    footerNote: 'Môi giới bất động sản được cấp phép',
    realtorLinkLabel: 'Hồ sơ Realtor.ca'
  },
  'zh-yue': {
    heroEyebrow: '住宅物業',
    heroIntro: '常駐滿地可的不動產經紀，重視清晰溝通與穩健協調。',
    ctaEmail: '電郵 Melissa',
    ctaListings: '查看放盤',
    languagesTitle: '語言',
    languagesIntro: '可提供以下語言服務：',
    languagesList: ['英文', '法文', '普通話', '越南話', '廣東話'],
    contactTitle: '聯絡',
    contactIntro: '準備好展開對話時，歡迎與我聯絡。',
    contactLabels: { email: '電郵', office: '寫字樓' },
    officeAddress: '700-413 Rue Saint-Jacques, 蒙特婁, QC H2Y 1N9',
    footerNote: '持牌房地產經紀',
    realtorLinkLabel: 'Realtor.ca 簡介'
  }
}

const currentLanguage = ref<LanguageId>(languageOptions[0].id)

const copy = computed(() => translations[currentLanguage.value])

const contactDetails = computed(() => [
  {
    label: copy.value.contactLabels.email,
    value: 'info@melissa-tran.com',
    href: 'mailto:info@melissa-tran.com'
  },
  {
    label: copy.value.contactLabels.office,
    value: copy.value.officeAddress,
    href: profileUrl
  }
])
</script>

<style scoped>
:global(body) {
  margin: 0;
  font-family: 'Space Grotesk', 'Inter', 'Helvetica Neue', Arial, sans-serif;
  background: #f6f6f3;
  color: #121212;
}

:global(*) {
  box-sizing: border-box;
}

.page {
  min-height: 100vh;
  padding: 3rem 1.5rem 2rem;
  max-width: 960px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.language-toggle {
  display: inline-flex;
  align-items: center;
  justify-content: flex-end;
  gap: 0.75rem;
  margin-left: auto;
}

.language-toggle__btn {
  border: none;
  background: none;
  color: #7a7a7a;
  padding: 0.15rem 0.25rem;
  font-size: 0.85rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  transition: color 0.2s ease;
  font-weight: 600;
  position: relative;
}

.language-toggle__btn::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: -0.3rem;
  height: 0.2rem;
  border-radius: 999px;
  background: transparent;
  transition: background 0.2s ease;
  z-index: -1;
}

.language-toggle__btn.active {
  color: #121212;
}

.language-toggle__btn.active::after {
  background: #7d776a;
}

.language-toggle__btn:hover {
  color: #121212;
}

.hero {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.hero__body {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
  flex-wrap: wrap;
}

.hero__text {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.hero__photo {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  overflow: hidden;
  border: 4px solid #ffffff;
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.08);
  flex-shrink: 0;
}

.hero__photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.hero__top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  flex-wrap: wrap;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: 0.85rem;
  color: #6f6f6f;
  margin: 0;
}

.hero__title {
  font-size: clamp(2.75rem, 6vw, 4rem);
  margin: 0;
}

.intro {
  font-size: 1.1rem;
  max-width: 40rem;
  color: #3a3a3a;
}

.cta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.cta a {
  text-decoration: none;
  font-weight: 600;
  padding: 0.9rem 1.5rem;
  border-radius: 999px;
  transition: background 0.2s ease, color 0.2s ease;
}

.primary {
  background: #121212;
  color: #f6f6f3;
}

.primary:hover {
  background: #000;
}

.secondary {
  color: #121212;
  border: 1px solid #d9d9d9;
}

.secondary:hover {
  border-color: #121212;
}

.panel {
  background: #ffffff;
  border: 1px solid #ebebeb;
  border-radius: 24px;
  padding: 2rem;
  display: grid;
  gap: 1.5rem;
}

.panel__content h2 {
  margin: 0 0 0.5rem;
}

.meta-label {
  text-transform: uppercase;
  letter-spacing: 0.15em;
  font-size: 0.75rem;
  color: #8b8b8b;
  margin-bottom: 0.5rem;
}

.languages__list {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  padding: 0;
  margin: 0;
}

.languages__list li {
  border: 1px solid #dcdcdc;
  border-radius: 999px;
  padding: 0.75rem 1.25rem;
  font-weight: 500;
  background: #fafafa;
}

.contact__details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.contact__details a {
  color: inherit;
  text-decoration: none;
  border-bottom: 1px solid transparent;
  padding-bottom: 0.1rem;
}

.contact__details a:hover {
  border-color: #121212;
}

footer {
  border-top: 1px solid #dcdcdc;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 0.5rem;
  padding-top: 1.5rem;
  font-size: 0.9rem;
  color: #525252;
}

footer a {
  color: inherit;
  text-decoration: none;
  border-bottom: 1px solid transparent;
}

footer a:hover {
  border-color: #121212;
}

@media (max-width: 768px) {
  .page {
    padding: 2.5rem 1.25rem;
  }

  .hero__body {
    flex-direction: column;
    align-items: flex-start;
  }

  .hero__top {
    flex-direction: column;
    align-items: flex-end;
    gap: 0.5rem;
  }

  .hero__photo {
    align-self: flex-start;
    order: -1;
  }

  .language-toggle {
    justify-content: flex-start;
    margin-left: 0;
    flex-wrap: wrap;
  }

  .panel {
    padding: 1.5rem;
  }
}
</style>
