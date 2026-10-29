<script setup lang="ts">
import { computed, ref, watch, onMounted } from 'vue'

import {
  GraduationCap, ArrowUpRight, Menu, X, Languages,
  Check, ArrowDown, BookOpen, Video, PlayCircle,
  CalendarDays, UserRound, Users, MessageCircle,
  ChevronDown, Sparkles, Headphones, Globe2,
  NotebookPen, Target, HeartHandshake, ClipboardCheck
} from 'lucide-vue-next'


type Lang = 'ar' | 'en'
const lang=ref<Lang>('ar')
const ar=computed(()=>lang.value==='ar')
const menuOpen=ref(false)
const openFaq=ref<number|null>(0)
const platformUrl=import.meta.env.VITE_PLATFORM_LOGIN_URL || ''
const whatsapp=(import.meta.env.VITE_PUBLIC_WHATSAPP || '').replace(/\D/g,'')
const email=import.meta.env.VITE_PUBLIC_EMAIL || ''
const words={
 ar:{navAbout:'عن الأكاديمية',navPrograms:'البرامج التعليمية',navFeatures:'المزايا',navFaq:'الأسئلة الشائعة',navContact:'تواصل معنا',login:'تسجيل الدخول',enroll:'اطلب استشارة تعليمية',eyebrow:'بيئة تعليمية تنمّي المعرفة والطموح',heroA:'تعلّم اليوم.',heroB:'وتقدّم بثقة.',heroDesc:'دروس تعليمية مباشرة عبر الإنترنت، فردية وجماعية، بإشراف معلمين يرافقون الطالب في رحلته التعليمية، مع تسجيلات ومواد تساعده على المراجعة والفهم في الوقت المناسب له.',discover:'اكتشف تجربتنا التعليمية',scroll:'تعرّف على المزيد',heroMini:'تعليم متاح لك أينما كنت',floatA:'حصص تعليمية تفاعلية',floatB:'من أي مكان',trustA:'حصص مباشرة',trustB:'تعليم مرن',trustC:'متابعة ومراجعة',strip:'رحلة تعليمية تُحدث فرقاً',strip2:'مصمّمة لتناسب أوقات الطلاب واحتياجاتهم',aboutEyebrow:'تعرّف على شام أكاديمي',aboutTitle:'أكثر من مجرد درس عبر الإنترنت؛ تجربة تعليمية متكاملة.',aboutDesc:'نؤمن بأن لكل طالب أسلوبه الخاص في التعلّم والاستيعاب. لذلك جمعنا الحصص المباشرة والموارد التعليمية في منصة واحدة منظّمة وسهلة الاستخدام.',aboutPoint1:'تواصل مباشر مع المعلّم',aboutPoint2:'الدروس والمواعيد في مكان واحد',aboutPoint3:'إمكانية مراجعة الحصص بعد انتهائها',programTag:'تعلّم بالطريقة التي تناسبك',programTitle:'اختر تجربتك التعليمية',programDesc:'سواء كنت تفضّل التركيز على احتياجاتك الفردية أو التعلّم والتفاعل مع زملائك، ستجد الخيار الملائم لأهدافك.',private:'دروس فردية',privateDesc:'حصة خاصة مع المعلّم تركّز على مستوى الطالب وأهدافه، وفق مواعيد تناسب احتياجاته.',privateLabel:'اهتمام فردي',group:'دروس جماعية',groupDesc:'تعلّم ضمن مجموعة منظّمة، واطرح الأسئلة وشارك في تجربة تعليمية تفاعلية مع زملائك.',groupLabel:'التعلّم التعاوني',ask:'استفسر عن البرنامج',featuresTag:'كل ما تحتاجه في مكان واحد',featuresTitle:'من الحصص المباشرة إلى المراجعة… جميع أدوات التعلّم بين يديك',featuresDesc:'تجربة تعليمية تستمر حتى بعد انتهاء الحصة.',f1:'حصص مباشرة',f1d:'تواصل مع المعلّم وشارك في الحصة عبر الإنترنت.',f2:'تسجيلات الحصص',f2d:'عُد إلى الشرح متى احتجت إلى المراجعة.',f3:'موارد تعليمية',f3d:'ملفات ومواد تساعدك على الدراسة والمراجعة.',f4:'جدول دراسي منظّم',f4d:'تعرّف على مواعيد حصصك بسهولة.',momentTag:'لحظات تصنع الفارق',momentTitle:'تصبح المعرفة أقرب عندما يكون التعلّم ممتعاً.',momentDesc:'بيئة تعليمية تشجّع على طرح الأسئلة والاستكشاف والمثابرة؛ فالنجاح يبدأ بخطوات صغيرة تتكرّر كل يوم.',journeyTag:'البداية بسيطة',journeyTitle:'من الاستفسار الأول إلى الحصة الأولى… ثلاث خطوات',step1:'تواصل معنا',step1d:'أخبرنا بالمرحلة الدراسية والمادة التي ترغب في دراستها.',step2:'اختر نوع الحصص',step2d:'نساعدك في اختيار البرنامج الفردي أو الجماعي الأنسب لاحتياجاتك.',step3:'ابدأ رحلتك التعليمية',step3d:'بعد تأكيد الاشتراك، ستصلك بيانات الدخول وجدول الحصص.',faqTag:'قبل أن تبدأ',faqTitle:'أسئلة قد تدور في ذهنك',faq1:'كيف يمكنني التسجيل في شام أكاديمي؟',faqa1:'اضغط على زر طلب الاشتراك وتواصل معنا. وبعد تحديد البرنامج المناسب، تنشئ إدارة الأكاديمية حساب الطالب.',faq2:'هل تتوفر دروس فردية وجماعية؟',faqa2:'نعم، توفّر الأكاديمية دروساً فردية بمواعيد مستقلة لكل طالب، ودروساً جماعية يشارك فيها عدة طلاب.',faq3:'هل يمكنني مراجعة تسجيلات الحصص؟',faqa3:'يمكن للطلاب المسجّلين تنزيل تسجيلات الحصص التي تتيحها إدارة الأكاديمية، وفقاً للتسجيلات المنشورة لكل حصة.',faq4:'كيف يمكنني الوصول إلى الحصص والملفات؟',faqa4:'بعد إتمام الاشتراك، تحصل على بيانات الدخول إلى المنصة، حيث يمكنك الاطلاع على حصصك ومواعيدها والملفات التعليمية المتاحة لك.',ctaEyebrow:'خطوتك التالية تبدأ هنا',ctaTitle:'هل أنت مستعد لبدء رحلة تعليمية متميزة؟',ctaDesc:'أخبرنا بالمادة الدراسية أو المستوى التعليمي الذي تحتاج إليه، وسنساعدك في اختيار البداية المناسبة.',contactWhats:'تواصل عبر واتساب',contactMail:'راسلنا عبر البريد الإلكتروني',contactNotSet:'يرجى إضافة رقم واتساب الأكاديمية أو بريدها الإلكتروني إلى ملف الإعدادات لتفعيل وسائل التواصل.',footDesc:'بيئة تعليمية متاحة لكل طالب أينما كان.',footQuick:'روابط مهمة',copyright:'جميع الحقوق محفوظة',contactUs:'التواصل',photoNote:'الصور توضيحية للتجربة التعليمية ولا تمثّل فريق الأكاديمية.', parentTag:'رسالة إلى أولياء الأمور',parentTitle:'اطمئنان لأولياء الأمور، وثقة أكبر للطلاب.',parentDesc:'يستطيع الطالب الاطلاع على مواعيد حصصه ومراجعة التسجيلات والملفات التعليمية من خلال حساب واحد منظّم؛ فالتعلّم الجيد يقوم على الوضوح والاستمرارية، ولا يقتصر على حصة دراسية واحدة.',parentA:'مسار دراسي واضح',parentB:'موارد متاحة بعد الحصة',parentC:'خيارات فردية وجماعية',subjectsTag:'المجالات التعليمية',subjectsTitle:'كل مرحلة من رحلة الطالب تستحق الدعم المناسب',subjectsDesc:'استفسر عن المواد والمراحل الدراسية المتاحة، وسنساعدك في اختيار البرنامج الأنسب وفقاً للخيارات الحالية.',subject1:'الرياضيات',subject2:'اللغة الإنجليزية',subject3:'العلوم',subject4:'مواد ومراحل دراسية أخرى',learningTag:'تعرّف على التجربة التعليمية',learningTitle:'تعليم أوضح، ومتابعة أسهل، وآفاق أوسع.',learningDesc:'حصص تفاعلية وتسجيلات منشورة وجدول منظّم يجمع كل ما يحتاجه الطالب في مكان واحد.',proofTag:'لماذا تختار شام أكاديمي؟',proofTitle:'تجربة مصمّمة للطلاب وتمنح أولياء الأمور الاطمئنان.',trustNote:'تُنشئ إدارة الأكاديمية حساب الطالب بعد إتمام إجراءات الاشتراك.',preview:'عرض توضيحي للتجربة التعليمية',parentAction:'استفسر عن البرنامج المناسب',finalNote:'ابدأ بالاستفسار، وسنوضّح لك خيارات الاشتراك المتاحة.'},
 en:{navAbout:'About us',navPrograms:'Programs',navFeatures:'Features',navFaq:'FAQ',navContact:'Contact',login:'Student login',enroll:'Ask about enrollment',eyebrow:'A brighter space to learn and grow',heroA:'Learn today.',heroB:'Grow with confidence.',heroDesc:'Live private and group online classes, supportive teachers, recordings, and resources to learn and revise at your own pace.',discover:'Explore the experience',scroll:'Discover more',heroMini:'Learning that meets you wherever you are',floatA:'Interactive classes',floatB:'Learn anywhere',trustA:'Live classes',trustB:'Flexible learning',trustC:'Review and repeat',strip:'Every learning journey matters',strip2:'Designed around students and their needs',aboutEyebrow:'Meet Sham Academy',aboutTitle:'More than an online lesson. A complete learning experience.',aboutDesc:'Every student learns differently. That is why we bring live lessons, educational resources and organized schedules together in one simple space.',aboutPoint1:'Direct contact with your teacher',aboutPoint2:'Lessons and schedules in one place',aboutPoint3:'Review lessons after class',programTag:'Learn in your own way',programTitle:'Find the right way to learn',programDesc:'From one-to-one support to learning with peers, choose what fits your goals.',private:'Private lessons',privateDesc:'Personal sessions focused on your progress, goals, and a schedule that works for you.',privateLabel:'Personalized attention',group:'Group lessons',groupDesc:'Learn together in structured sessions, ask questions and grow with other students.',groupLabel:'Collaborative learning',ask:'Explore this program',featuresTag:'Everything in one place',featuresTitle:'From live lessons to revision, it’s all here.',featuresDesc:'Learning continues beyond the live session.',f1:'Live classes',f1d:'Meet and interact with your teacher online.',f2:'Lesson recordings',f2d:'Revisit published lessons at your pace.',f3:'Learning resources',f3d:'PDFs and supporting study materials.',f4:'Organized schedule',f4d:'Keep track of upcoming sessions easily.',momentTag:'Moments that matter',momentTitle:'Learning feels closer when curiosity leads.',momentDesc:'A learning environment where questions are welcome and progress comes through small, consistent steps.',journeyTag:'Getting started',journeyTitle:'From first hello to first lesson in three steps',step1:'Get in touch',step1d:'Tell us your school level and what you want to learn.',step2:'Find your fit',step2d:'We help you choose a private or group program.',step3:'Start learning',step3d:'After enrollment, receive your login details and class schedule.',faqTag:'Before you begin',faqTitle:'Frequently asked questions',faq1:'How do I enroll at Sham Academy?',faqa1:'Contact us through the enrollment button. After you choose a program, our administrator creates the student account.',faq2:'Are both private and group lessons available?',faqa2:'Yes. Private lessons use individual student schedules, while group lessons bring students together.',faq3:'Can I watch lesson recordings?',faqa3:'Enrolled students can download recordings published by the administrator for their lessons.',faq4:'How do I access lessons and materials?',faqa4:'After enrollment, use your student account to access your schedules, lessons and available files.',ctaEyebrow:'Your next chapter starts here',ctaTitle:'Ready for a better way to learn?',ctaDesc:'Tell us your learning goals and we will help you find the right starting point.',contactWhats:'Message on WhatsApp',contactMail:'Email us',contactNotSet:'Set your academy WhatsApp number or email in the environment file to enable contact.',footDesc:'Learning made closer, wherever you are.',footQuick:'Quick links',copyright:'All rights reserved',contactUs:'Contact',photoNote:'Images illustrate the learning experience and do not portray academy staff.',parentTag:'For every parent',parentTitle:'Peace of mind for parents. Confidence for learners.',parentDesc:'Students can check lessons, revisit published recordings, and access materials in one organized account. Because great learning is built on clarity and consistency.',parentA:'Clear lesson schedules',parentB:'Materials after class',parentC:'Private and group options',subjectsTag:'Learning areas',subjectsTitle:'Every step of learning deserves the right support',subjectsDesc:'Ask us about currently available subjects and school levels, and we will help identify the best fit.',subject1:'Mathematics',subject2:'English language',subject3:'Science',subject4:'Other subjects & levels',learningTag:'The learning experience',learningTitle:'Clearer learning. Easier follow-up. Brighter futures.',learningDesc:'Interactive live classes, published recordings and a simple schedule all in one place.',proofTag:'Why Sham Academy',proofTitle:'Built for students. Reassuring for parents.',trustNote:'Student accounts are created by academy administrators after enrollment.',preview:'Illustration of the learning experience',parentAction:'Ask about the right program',finalNote:'Start with a simple question, and we will explain your enrollment options.'}
}
const t=computed(()=>words[lang.value])
const nav=computed(()=>[{id:'about',label:t.value.navAbout},{id:'programs',label:t.value.navPrograms},{id:'pricing',label:ar.value?'الباقات والأسعار':'Pricing'},{id:'features',label:t.value.navFeatures},{id:'faq',label:t.value.navFaq}])
const features=computed(()=>[{icon:Video,title:t.value.f1,desc:t.value.f1d},{icon:PlayCircle,title:t.value.f2,desc:t.value.f2d},{icon:BookOpen,title:t.value.f3,desc:t.value.f3d},{icon:CalendarDays,title:t.value.f4,desc:t.value.f4d}])
const faqs=computed(()=>[{q:t.value.faq1,a:t.value.faqa1},{q:t.value.faq2,a:t.value.faqa2},{q:t.value.faq3,a:t.value.faqa3},{q:t.value.faq4,a:t.value.faqa4}])
const waUrl=computed(()=>whatsapp?`https://wa.me/${whatsapp}?text=${encodeURIComponent(ar.value?'مرحباً، أودّ الاستفسار عن البرامج التعليمية المتاحة في شام أكاديمي وآلية الاشتراك فيها':'Hello, I would like to learn about Sham Academy programs and enrollment.')}`:'')
// Pricing plans for the public landing page (independent from the LMS backend).
const pricingText = computed(() => ar.value ? ({
  kicker: 'باقات تعليمية تلائم احتياجاتك',
  heading: 'استثمر في تعليم أبنائك بخيارات واضحة',
  intro: 'ابدأ بتقييم مجاني للمستوى، ثم اختر الدعم المناسب: حصة واحدة أو متابعة منتظمة طوال الفصل الدراسي.',
  from: 'ابتداءً من',
  currency: 'ر.س',
  perLesson: '/ للحصة',
  free: 'مجاناً',
  freeDetail: 'دون رسوم',
  diagnostic: 'باقة تقييم المستوى المجانية',
  diagnosticDesc: 'تعرّف على المستوى الحالي للطالب في المادة الدراسية التي يختارها.',
  single: 'باقة الحصة المرنة',
  singleDesc: 'حصة مركّزة في موضوع دراسي محدّد، ويُحدّد سعرها وفقاً للدرس المطلوب.',
  subject: 'باقة المتابعة الفصلية',
  subjectDesc: 'متابعة تعليمية مع معلّم متخصص في مادة دراسية واحدة طوال الفصل الدراسي.',
  all: 'باقة التفوّق الشامل',
  allDesc: 'دعم تعليمي شامل ومتابعة منظّمة في جميع المواد الدراسية.',
  starter: 'اطلب التقييم المجاني',
  enroll: 'استفسر عن الباقة',
  featured: 'متابعة طوال الفصل الدراسي',
  assessA: 'حصة لتقييم مستوى الطالب',
  assessB: 'أسئلة تقييم في المادة المختارة',
  assessC: 'تحديد نقاط القوة والجوانب التي تحتاج إلى تطوير',
  singleA: 'الدفع مقابل كل حصة على حدة',
  singleB: 'اختيار المادة والموضوع الدراسي المطلوب',
  singleC: 'تحديد السعر النهائي وفقاً للحصة',
  subjectA: 'متابعة في مادة دراسية واحدة',
  subjectB: 'إشراف معلّم طوال الفصل الدراسي',
  subjectC: 'خطة حصص تراعي احتياجات الطالب',
  allA: 'متابعة تعليمية في جميع المواد',
  allB: 'دعم دراسي متكامل',
  allC: 'تنظيم الحصص وفقاً للمواد والمستوى الدراسي',
  note: 'الأسعار الموضّحة هي أسعار ابتدائية بالريال السعودي. يُحدّد السعر النهائي وتفاصيل الحصص وشروط الاشتراك عند التواصل مع الأكاديمية.',
  request: 'مرحباً، أودّ الاستفسار عن باقة',
}) : ({
  kicker: 'Plans for every learning journey',
  heading: 'A smarter investment in your child’s learning',
  intro: 'Start with a free level assessment, then choose a single lesson or ongoing semester support.',
  from: 'From',
  currency: 'SAR',
  perLesson: '/ lesson',
  free: 'Free',
  freeDetail: 'No charge',
  diagnostic: 'Learning Level Check',
  diagnosticDesc: 'Find the right starting point in the student’s chosen subject.',
  single: 'Pay Per Lesson',
  singleDesc: 'Focused support for a specific lesson, priced according to the topic.',
  subject: 'Semester Subject Mentor',
  subjectDesc: 'Teacher-led guidance for one subject throughout the semester.',
  all: 'Complete Learning Journey',
  allDesc: 'Ongoing academic support across all school subjects.',
  starter: 'Get assessed for free',
  enroll: 'Ask about this plan',
  featured: 'Full-semester support',
  assessA: 'A lesson to evaluate current level',
  assessB: 'Subject-specific assessment questions',
  assessC: 'Identify strengths and areas to improve',
  singleA: 'Pay for individual lessons',
  singleB: 'Choose your subject and topic',
  singleC: 'Final price depends on the lesson',
  subjectA: 'One school subject',
  subjectB: 'Semester-long teacher guidance',
  subjectC: 'Lessons planned around student needs',
  allA: 'Coverage across all subjects',
  allB: 'Comprehensive academic support',
  allC: 'Study plans tailored to needs and subjects',
  note: 'Starting prices are in Saudi riyals. Final pricing and lesson details are confirmed with the academy.',
  request: 'Hello, I would like to ask about the plan',
}))
const pricingPlans = computed(() => {
  const p = pricingText.value
  return [
    { id: 'assessment', icon: ClipboardCheck, title: p.diagnostic, desc: p.diagnosticDesc,
      price: '0', prefix: '', suffix: p.freeDetail, items: [p.assessA, p.assessB, p.assessC], cta: p.starter, featured: false },
    { id: 'lesson', icon: BookOpen, title: p.single, desc: p.singleDesc,
      price: '79.9', prefix: p.from, suffix: p.perLesson, items: [p.singleA, p.singleB, p.singleC], cta: p.enroll, featured: false },
    { id: 'semester', icon: UserRound, title: p.subject, desc: p.subjectDesc,
      price: '64.9', prefix: p.from, suffix: p.perLesson, items: [p.subjectA, p.subjectB, p.subjectC], cta: p.enroll, featured: true },
    { id: 'complete', icon: GraduationCap, title: p.all, desc: p.allDesc,
      price: '54.9', prefix: p.from, suffix: ar.value ? '/ للساعة التعليمية' : '/ teaching hour', items: [p.allA, p.allB, p.allC], cta: p.enroll, featured: false },
  ]
})
function planUrl(name: string) {
  if (!whatsapp) return '#contact'
  return `https://wa.me/${whatsapp}?text=${encodeURIComponent(`${pricingText.value.request} ${name}.`)}`
}
const photos={
 hero:'https://images.unsplash.com/photo-1523240795612-9a054b0db644?auto=format&fit=crop&w=2200&q=90',
 private:'https://images.unsplash.com/photo-1434030216411-0b793f4b4173?auto=format&fit=crop&w=1800&q=90',
group: `${import.meta.env.BASE_URL}images/group.webp`,
 about:'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=1900&q=90',
 moment:'https://images.unsplash.com/photo-1503676260728-1c00da094a0b?auto=format&fit=crop&w=1900&q=90',
 portrait:'https://images.unsplash.com/photo-1491013516836-7db643ee125a?auto=format&fit=crop&w=900&q=85'
}
function imageFallback(event: Event, fallback: string){ const element = event.target as HTMLImageElement; if(!element.src.endsWith(fallback)){element.onerror=null;element.src=fallback} }
function setLanguage(){lang.value=ar.value?'en':'ar';menuOpen.value=false}
function goTop(){window.scrollTo({top:0,behavior:'smooth'});menuOpen.value=false}
watch(lang,value=>{document.documentElement.lang=value;document.documentElement.dir=value==='ar'?'rtl':'ltr';document.title=value==='ar'?'شام أكاديمي | تعلّم بثقة':'Sham Academy | Learn with confidence'})
onMounted(()=>{document.documentElement.lang=lang.value;document.documentElement.dir='rtl'})
</script>
<template>
<div :dir="ar?'rtl':'ltr'" class="overflow-x-hidden bg-[#f8faff] text-[#102654]">
  <header class="sticky top-0 z-50 border-b border-[#e2e8f0] bg-[#f8faff]/95 backdrop-blur-xl">
    <nav class="mx-auto flex h-[86px] max-w-[1400px] items-center justify-between gap-5 px-5 md:px-10">
      <a href="#top" class="flex shrink-0 items-center gap-3" @click="menuOpen=false"><span class="grid h-11 w-11 place-items-center rounded-2xl bg-[#2563eb] text-white shadow-lg shadow-[#2563eb]/15"><GraduationCap :size="24"/></span><span class="text-xl font-black tracking-tight" dir="ltr">Sham<span class="text-[#60a5fa]">.</span>Academy</span></a>
      <div class="hidden items-center gap-9 lg:flex"><a v-for="item in nav" :key="item.id" :href="'#'+item.id" class="text-[13px] font-bold text-[#344054] transition hover:text-[#124295]">{{item.label}}</a></div>
      <div class="flex items-center gap-2 md:gap-3"><button type="button" class="flex items-center gap-1.5 rounded-full border border-[#dbeafe] bg-white px-3 py-2.5 text-xs font-bold hover:bg-[#eff6ff]" @click="setLanguage"><Languages :size="17"/>{{ar?'EN':'AR'}}</button><a v-if="platformUrl" :href="platformUrl" class="hidden text-[13px] font-bold hover:text-[#1d4a98] sm:inline">{{t.login}}</a><a href="#contact" class="hidden rounded-full bg-[#102654] px-5 py-3 text-xs font-extrabold text-white transition hover:bg-[#1d4ed8] sm:inline-flex">{{t.enroll}} <ArrowUpRight :size="16" class="ms-2"/></a><button type="button" :aria-label="menuOpen?'Close menu':'Open menu'" class="rounded-xl p-2 lg:hidden" @click="menuOpen=!menuOpen"><X v-if="menuOpen" :size="23"/><Menu v-else :size="23"/></button></div>
    </nav>
    <div v-if="menuOpen" class="border-t bg-white px-6 py-4 lg:hidden"><a v-for="item in nav" :key="item.id" :href="'#'+item.id" class="block rounded-xl p-3 font-semibold hover:bg-[#eff6ff]" @click="menuOpen=false">{{item.label}}</a><a href="#contact" class="block rounded-xl p-3 font-extrabold text-[#153a7a]" @click="menuOpen=false">{{t.enroll}}</a><a v-if="platformUrl" :href="platformUrl" class="block p-3 font-semibold">{{t.login}}</a></div>
  </header>
  <main id="top">
    <section class="relative overflow-hidden bg-gradient-to-br from-[#f5f9ff] via-[#eaf3ff] to-[#dbeaff]">
      <div class="pointer-events-none absolute -start-44 -top-32 h-96 w-96 rounded-full bg-[#b3d1ff] blur-3xl"></div>
      <div class="relative mx-auto grid max-w-[1400px] items-center gap-10 px-5 py-12 md:px-10 lg:min-h-[740px] lg:grid-cols-[.93fr_1.07fr] lg:gap-14 lg:py-18">
        <div class="reveal relative z-10 py-8 lg:py-14"><div class="mb-8 inline-flex items-center gap-2.5 rounded-full border border-[#cfd9e7] bg-white/85 px-4 py-2 text-xs font-extrabold text-[#244276]"><Sparkles :size="16"/> {{t.eyebrow}}</div><h1 class="max-w-2xl text-[clamp(2.8rem,5vw,5.65rem)] leading-[1.24] font-black tracking-tight">{{t.heroA}}<span class="block text-[#2563eb]">{{t.heroB}}</span></h1><p class="mt-6 max-w-[570px] text-[15px] leading-[2.1] font-semibold text-[#64748b] md:text-lg">{{t.heroDesc}}</p><div class="mt-9 flex flex-wrap gap-3"><a href="#contact" class="inline-flex items-center gap-3 rounded-full bg-[#2563eb] px-8 py-4 text-sm font-extrabold text-white shadow-xl shadow-[#2563eb]/15 transition hover:-translate-y-1 hover:bg-[#1d4ed8]">{{t.enroll}}<ArrowUpRight :size="20"/></a><a href="#programs" class="inline-flex items-center gap-2 rounded-full border border-[#c5d0df] bg-white px-7 py-4 text-sm font-bold transition hover:bg-[#f9fbfe]">{{t.discover}}<ArrowDown :size="18"/></a></div><div class="mt-11 grid max-w-md grid-cols-3 gap-2 border-t border-[#ced7e2] pt-7"><div v-for="(txt,i) in [t.trustA,t.trustB,t.trustC]" :key="i" class="flex flex-col items-start gap-2"><span class="grid h-8 w-8 place-items-center rounded-full bg-white text-[#2563eb]"><Check :size="17" stroke-width="3"/></span><span class="text-xs leading-5 font-extrabold text-[#475569]">{{txt}}</span></div></div></div>
        <div class="reveal relative min-h-[420px] self-stretch lg:min-h-[625px]"><div class="image-zoom absolute inset-0 overflow-hidden rounded-[35px] shadow-2xl shadow-[#102654]/25 lg:rounded-[54px] ring-8 ring-white/70"><img :src="photos.hero" @error="imageFallback($event, '/images/hero.webp')" alt="Students studying together with laptops" class="h-full w-full object-cover" fetchpriority="high"/><div class="absolute inset-0 bg-gradient-to-t from-[#0b1c40]/35 via-transparent to-transparent"></div></div><div class="absolute bottom-7 start-5 flex items-center gap-3 rounded-2xl border border-white/60 bg-white/95 px-5 py-4 shadow-2xl backdrop-blur-md sm:start-[-25px]"><span class="grid h-11 w-11 place-items-center rounded-xl bg-[#dbeafe] text-[#163e85]"><Video :size="22"/></span><span><strong class="block text-sm font-black">{{t.floatA}}</strong><span class="text-xs text-[#5e7899]">{{t.floatB}}</span></span></div></div>
      </div>
    </section>
    <div class="bg-[#102654] px-6 py-6 text-center text-white"><div class="mx-auto flex max-w-6xl flex-wrap items-center justify-center gap-3 text-xs font-bold tracking-wide md:gap-8 md:text-sm"><span class="text-[#93c5fd]">✦</span><span>{{t.strip}}</span><span class="opacity-35">/</span><span>{{t.strip2}}</span><span class="text-[#93c5fd]">✦</span></div></div>
    <section id="about" class="scroll-mt-24 mx-auto grid max-w-[1400px] items-center gap-14 px-5 py-24 md:px-10 lg:grid-cols-2 lg:py-32"><div class="relative order-2 lg:order-1"><div class="image-zoom relative h-[420px] overflow-hidden rounded-[35px] md:h-[540px]"><img :src="photos.about" @error="imageFallback($event, '/images/about.webp')" alt="Students working collaboratively on a computer" class="h-full w-full object-cover" loading="lazy"/></div><div class="absolute -bottom-6 end-5 flex items-center gap-3 rounded-2xl bg-[#dbeafe] px-6 py-5 shadow-lg lg:-end-7"><Headphones :size="30" class="text-[#1e3f7a]"/><span class="max-w-40 text-sm leading-6 font-extrabold">{{t.heroMini}}</span></div></div><div class="order-1 lg:order-2"><p class="mb-4 text-xs font-black tracking-widest text-[#124091]">{{t.aboutEyebrow}}</p><h2 class="max-w-xl text-3xl leading-[1.5] font-black sm:text-5xl">{{t.aboutTitle}}</h2><p class="mt-6 max-w-xl text-[15px] leading-9 font-semibold text-[#64748b]">{{t.aboutDesc}}</p><div class="mt-9 space-y-5"><div v-for="point in [t.aboutPoint1,t.aboutPoint2,t.aboutPoint3]" :key="point" class="flex items-center gap-4"><span class="grid h-10 w-10 shrink-0 place-items-center rounded-full bg-[#dbeafe] text-[#123d88]"><Check :size="20" stroke-width="3"/></span><span class="text-sm font-extrabold">{{point}}</span></div></div></div></section>
    <!-- Premium parent-confidence section -->
    <section class="relative overflow-hidden bg-white px-5 py-24 md:px-10 lg:py-32">
      <div class="pointer-events-none absolute -end-32 top-1/4 h-96 w-96 rounded-full bg-blue-100/70 blur-3xl"></div>
      <div class="relative mx-auto grid max-w-[1400px] items-center gap-12 lg:grid-cols-[.96fr_1.04fr] lg:gap-20">
        <div>
          <p class="section-kicker"><HeartHandshake :size="17" />{{t.parentTag}}</p>
          <h2 class="mt-5 max-w-2xl text-4xl font-black leading-[1.5] tracking-tight sm:text-5xl">{{t.parentTitle}}</h2>
          <p class="mt-6 max-w-xl text-base leading-9 text-slate-600">{{t.parentDesc}}</p>
          <div class="mt-8 grid gap-4 sm:grid-cols-3">
            <div v-for="(point,i) in [t.parentA,t.parentB,t.parentC]" :key="point" class="rounded-2xl border border-blue-100 bg-[#f4f8ff] p-5 shadow-sm transition hover:shadow-lg">
              <span class="mb-4 grid h-11 w-11 place-items-center rounded-xl bg-white text-[#2563eb]"><component :is="[ClipboardCheck,BookOpen,Users][i]" :size="23" /></span>
              <p class="text-[13px] font-extrabold leading-7">{{point}}</p>
            </div>
          </div>
          <a href="#contact" class="mt-9 inline-flex items-center gap-2 text-sm font-black text-[#1d4ed8] hover:underline">{{t.parentAction}} <ArrowUpRight :size="19" /></a>
        </div>
        <div class="relative rounded-[38px] bg-gradient-to-br from-[#102654] via-[#153f89] to-[#2563eb] p-6 shadow-2xl shadow-blue-950/20 sm:p-9">
          <div class="flex items-center justify-between gap-3 text-white"><span class="flex items-center gap-2 text-sm font-extrabold"><GraduationCap :size="23"/> Sham Academy</span><span class="rounded-full bg-white/15 px-3 py-1.5 text-xs">{{t.preview}}</span></div>
          <div class="mt-7 grid gap-4 sm:grid-cols-[1.2fr_.8fr]">
            <div class="relative overflow-hidden rounded-3xl bg-white/10"><img src="/images/private.webp" class="h-72 w-full object-cover" alt="Student learning online" loading="lazy"/><div class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-[#061737]/80 to-transparent p-5"><p class="text-lg font-black text-white">{{t.f1}}</p></div></div>
            <div class="grid gap-4"><div class="rounded-3xl bg-white p-5"><Video class="mb-3 text-blue-600" :size="26"/><h3 class="text-sm font-black">{{t.f1}}</h3><p class="mt-2 text-xs leading-6 text-slate-500">{{t.f1d}}</p></div><div class="rounded-3xl bg-[#dbeafe] p-5"><PlayCircle class="mb-3 text-blue-700" :size="26"/><h3 class="text-sm font-black">{{t.f2}}</h3><p class="mt-2 text-xs leading-6 text-slate-600">{{t.f2d}}</p></div></div>
          </div>
          <p class="mt-5 text-xs leading-6 text-blue-100">{{t.trustNote}}</p>
        </div>
      </div>
    </section>
    <!-- Available subjects inquiry -->
    <section class="border-y border-blue-100 bg-[#f5f9ff] px-5 py-20 md:px-10">
      <div class="mx-auto max-w-[1400px]"><div class="flex flex-wrap items-end justify-between gap-8"><div><p class="section-kicker"><NotebookPen :size="18"/>{{t.subjectsTag}}</p><h2 class="mt-4 max-w-3xl text-3xl font-black leading-[1.5] sm:text-5xl">{{t.subjectsTitle}}</h2></div><p class="max-w-sm text-sm leading-8 text-slate-600">{{t.subjectsDesc}}</p></div>
        <div class="mt-12 grid gap-4 sm:grid-cols-2 lg:grid-cols-4"><a v-for="(label,i) in [t.subject1,t.subject2,t.subject3,t.subject4]" :key="label" href="#contact" class="group flex min-h-36 flex-col justify-between rounded-3xl border border-blue-100 bg-white p-6 shadow-sm transition duration-300 hover:-translate-y-2 hover:border-blue-300 hover:shadow-xl"><span class="flex items-center justify-between"><span class="grid h-12 w-12 place-items-center rounded-2xl bg-[#eff6ff] text-[#2563eb]"><component :is="[Target,Globe2,Sparkles,BookOpen][i]" :size="25" /></span><ArrowUpRight :size="20" class="text-slate-400 transition group-hover:text-[#2563eb]"/></span><span class="text-lg font-black">{{label}}</span></a></div>
      </div>
    </section>
    <section id="programs" class="scroll-mt-24 bg-[#eef5ff] px-5 py-24 md:px-10 lg:py-30"><div class="mx-auto max-w-[1400px]"><div class="mb-12 grid items-end gap-5 lg:grid-cols-2"><div><p class="mb-3 text-xs font-black tracking-widest text-[#1a4796]">{{t.programTag}}</p><h2 class="max-w-xl text-3xl leading-[1.45] font-black sm:text-5xl">{{t.programTitle}}</h2></div><p class="max-w-lg text-[15px] leading-9 font-semibold text-[#64748b]">{{t.programDesc}}</p></div><div class="grid gap-6 md:grid-cols-2"><article v-for="(program,i) in [{photo:photos.private,label:t.privateLabel,title:t.private,desc:t.privateDesc,icon:UserRound},{photo:photos.group,label:t.groupLabel,title:t.group,desc:t.groupDesc,icon:Users}]" :key="i" class="group image-zoom overflow-hidden rounded-[30px] bg-white shadow-sm transition hover:-translate-y-2 hover:shadow-2xl hover:shadow-[#1e3a8a]/15 duration-500"><div class="relative h-64 overflow-hidden md:h-[310px]"><img :src="program.photo" @error="imageFallback($event, i === 0 ? '/images/private.webp' : '/images/group.webp')" :alt="program.title" loading="lazy" class="h-full w-full object-cover"/><span class="absolute bottom-5 start-5 rounded-full bg-white/95 px-5 py-2 text-xs font-black text-[#193565] shadow-md">{{program.label}}</span></div><div class="p-7 md:p-9"><div class="flex items-center justify-between"><span class="grid h-12 w-12 place-items-center rounded-xl bg-[#eff6ff] text-[#163e85]"><component :is="program.icon" :size="25"/></span><span class="text-sm font-extrabold text-[#839bb9]">0{{i+1}}</span></div><h3 class="mt-5 text-2xl font-black">{{program.title}}</h3><p class="mt-3 max-w-lg text-sm leading-8 font-semibold text-[#64748b]">{{program.desc}}</p><a href="#contact" class="mt-5 inline-flex items-center gap-2 text-sm font-black text-[#133e8a]">{{t.ask}} <ArrowUpRight :size="19"/></a></div></article></div></div></section>

    <!-- Pricing packages: four clear plans, in Arabic and English -->
    <section id="pricing" class="scroll-mt-24 relative overflow-hidden bg-[#f4f8ff] px-5 py-24 md:px-10 lg:py-32">
      <div class="pointer-events-none absolute -top-36 -end-24 h-96 w-96 rounded-full bg-blue-200/45 blur-3xl"></div>
      <div class="pointer-events-none absolute -bottom-40 -start-24 h-96 w-96 rounded-full bg-indigo-200/30 blur-3xl"></div>
      <div class="relative mx-auto max-w-[1400px]">
        <div class="mx-auto max-w-3xl text-center">
          <span class="inline-flex items-center gap-2 rounded-full border border-blue-200 bg-white px-5 py-2 text-xs font-extrabold text-blue-700 shadow-sm">
            <Sparkles :size="16" />{{ pricingText.kicker }}
          </span>
          <h2 class="mt-6 text-3xl font-black leading-[1.5] text-[#102654] sm:text-5xl">{{ pricingText.heading }}</h2>
          <p class="mx-auto mt-5 max-w-2xl text-sm leading-8 text-slate-600 sm:text-base">{{ pricingText.intro }}</p>
        </div>

        <div class="mt-14 grid items-stretch gap-5 md:grid-cols-2 xl:grid-cols-4">
          <article
            v-for="plan in pricingPlans"
            :key="plan.id"
            class="group relative flex flex-col overflow-hidden rounded-[30px] border bg-white p-7 transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl sm:p-8"
            :class="plan.featured
              ? 'border-blue-500 shadow-xl shadow-blue-600/15 ring-2 ring-blue-500 xl:-translate-y-3 xl:hover:-translate-y-5'
              : 'border-blue-100 shadow-sm hover:border-blue-300 hover:shadow-blue-900/10'"
          >
            <div v-if="plan.featured" class="absolute inset-x-0 top-0 h-1.5 bg-gradient-to-r from-blue-600 via-cyan-400 to-blue-600"></div>
            <div class="flex min-h-10 items-center justify-between gap-2">
              <span class="grid h-14 w-14 place-items-center rounded-2xl bg-blue-50 text-blue-600 transition group-hover:bg-blue-600 group-hover:text-white">
                <component :is="plan.icon" :size="27" />
              </span>
              <span v-if="plan.featured" class="rounded-full bg-blue-600 px-3 py-1.5 text-[11px] font-extrabold text-white">{{ pricingText.featured }}</span>
            </div>

            <h3 class="mt-7 min-h-16 text-[21px] font-black leading-[1.6] text-[#102654]">{{ plan.title }}</h3>
            <p class="mt-2 min-h-24 text-sm leading-7 text-slate-500">{{ plan.desc }}</p>

            <div class="my-6 border-y border-blue-100 py-6">
              <p v-if="plan.prefix" class="mb-1 text-xs font-bold text-slate-500">{{ plan.prefix }}</p>
              <div v-if="plan.id === 'assessment'" class="text-[42px] font-black leading-tight tracking-tight text-blue-600">{{ pricingText.free }}</div>
              <div v-else class="flex flex-wrap items-baseline gap-2" dir="ltr">
                <strong class="text-[43px] font-black leading-tight tracking-tight text-[#102654]">{{ plan.price }}</strong>
                <span class="text-sm font-extrabold text-blue-600">{{ pricingText.currency }}</span>
              </div>
              <p class="mt-1 text-xs font-semibold text-slate-500">{{ plan.suffix }}</p>
            </div>

            <ul class="mb-8 flex-1 space-y-4">
              <li v-for="item in plan.items" :key="item" class="flex items-start gap-3 text-[13px] font-semibold leading-7 text-slate-700">
                <span class="mt-1 grid h-6 w-6 shrink-0 place-items-center rounded-full bg-blue-50 text-blue-600">
                  <Check :size="14" stroke-width="3" />
                </span>
                <span>{{ item }}</span>
              </li>
            </ul>

            <a
              :href="planUrl(plan.title)"
              :target="whatsapp ? '_blank' : undefined"
              :rel="whatsapp ? 'noopener noreferrer' : undefined"
              class="flex min-h-13 items-center justify-center gap-2 rounded-2xl px-5 py-3.5 text-center text-sm font-extrabold transition hover:-translate-y-0.5"
              :class="plan.featured
                ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/20 hover:bg-blue-700'
                : 'bg-[#102654] text-white hover:bg-blue-700'"
            >
              {{ plan.cta }}
              <ArrowUpRight :size="18" />
            </a>
          </article>
        </div>
        <p class="mx-auto mt-9 max-w-4xl text-center text-xs leading-7 text-slate-500">{{ pricingText.note }}</p>
      </div>
    </section>
    <section id="features" class="scroll-mt-24 mx-auto max-w-[1400px] px-5 py-24 md:px-10 lg:py-30"><div class="mx-auto max-w-3xl text-center"><p class="mb-3 text-xs font-black tracking-widest text-[#2563eb]">{{t.featuresTag}}</p><h2 class="text-3xl leading-[1.45] font-black sm:text-5xl">{{t.featuresTitle}}</h2><p class="mt-5 text-base text-[#64748b]">{{t.featuresDesc}}</p></div><div class="mt-14 grid gap-5 sm:grid-cols-2 lg:grid-cols-4"><article v-for="(feature,i) in features" :key="feature.title" class="rounded-3xl border border-[#e2e8f0] bg-white p-7 transition hover:-translate-y-1 hover:border-[#a3bcdc] hover:shadow-xl hover:shadow-[#1e3a8a]/10"><span class="grid h-14 w-14 place-items-center rounded-2xl" :class="i%2===0?'bg-[#dbeafe] text-[#133a7f]':'bg-[#eff6ff] text-[#2563eb]'"><component :is="feature.icon" :size="27"/></span><h3 class="mt-7 text-lg font-black">{{feature.title}}</h3><p class="mt-3 text-sm leading-8 text-[#64748b]">{{feature.desc}}</p></article></div></section>
    <section class="relative overflow-hidden bg-[#102654] text-white"><div class="grid min-h-[460px] lg:grid-cols-2"><div class="px-7 py-18 md:px-16 lg:py-24"><div class="mx-auto max-w-xl"><p class="mb-5 text-xs font-black tracking-widest text-[#93c5fd]">{{t.momentTag}}</p><h2 class="text-3xl leading-[1.5] font-black sm:text-5xl">{{t.momentTitle}}</h2><p class="mt-7 max-w-lg text-base leading-9 text-[#bfdbfe]">{{t.momentDesc}}</p><a href="#contact" class="mt-9 inline-flex items-center gap-2 rounded-full bg-white px-6 py-3 text-sm font-black text-[#173261] transition hover:bg-[#dbeafe]">{{t.enroll}} <ArrowUpRight :size="18"/></a></div></div><div class="relative min-h-80 overflow-hidden"><img :src="photos.moment" @error="imageFallback($event, '/images/moment.webp')" alt="Students enjoying learning in classroom" loading="lazy" class="absolute inset-0 h-full w-full object-cover"/><div class="absolute inset-0 bg-[#102654]/10"></div></div></div></section>
    <section id="journey" class="mx-auto max-w-[1400px] px-5 py-24 md:px-10 lg:py-30"><div class="text-center"><p class="mb-3 text-xs font-black tracking-widest text-[#2563eb]">{{t.journeyTag}}</p><h2 class="text-3xl leading-[1.5] font-black sm:text-5xl">{{t.journeyTitle}}</h2></div><div class="mt-14 grid gap-6 md:grid-cols-3"><div v-for="(step,i) in [{title:t.step1,desc:t.step1d},{title:t.step2,desc:t.step2d},{title:t.step3,desc:t.step3d}]" :key="step.title" class="relative rounded-3xl bg-[#eff6ff] p-8 md:p-10"><div class="mb-7 grid h-14 w-14 place-items-center rounded-full bg-[#2563eb] text-xl font-black text-white">{{String(i+1).padStart(2,'0')}}</div><h3 class="text-xl font-black">{{step.title}}</h3><p class="mt-4 text-sm leading-8 text-[#64748b]">{{step.desc}}</p></div></div></section>
    <section id="faq" class="scroll-mt-24 bg-[#eff6ff] px-5 py-24 md:px-10"><div class="mx-auto grid max-w-[1300px] gap-10 lg:grid-cols-[.8fr_1.2fr] lg:gap-24"><div><p class="mb-3 text-xs font-black tracking-widest text-[#2563eb]">{{t.faqTag}}</p><h2 class="text-3xl leading-[1.5] font-black sm:text-5xl">{{t.faqTitle}}</h2><div class="mt-7 h-1 w-20 rounded-full bg-[#60a5fa]"></div></div><div class="space-y-3"><div v-for="(faq,i) in faqs" :key="i" class="overflow-hidden rounded-2xl border border-[#e2e8f0] bg-white"><button type="button" :aria-expanded="openFaq===i" class="flex w-full items-center justify-between gap-4 px-6 py-5 text-start text-sm font-black sm:text-base" @click="openFaq=openFaq===i?null:i"><span>{{faq.q}}</span><ChevronDown :size="20" class="shrink-0 text-[#2563eb] transition-transform" :class="openFaq===i?'rotate-180':''"/></button><div v-if="openFaq===i" class="border-t border-[#e2e8f0] px-6 py-5 text-sm leading-8 text-[#64748b]">{{faq.a}}</div></div></div></div></section>
    <section id="contact" class="scroll-mt-24 px-5 py-20 md:px-10"><div class="relative mx-auto max-w-[1400px] overflow-hidden rounded-[36px] bg-[#102654] px-6 py-16 text-center text-white md:py-24"><div class="pointer-events-none absolute -end-16 -top-24 h-72 w-72 rounded-full border border-white/15"></div><div class="pointer-events-none absolute -start-20 -bottom-48 h-96 w-96 rounded-full border border-white/10"></div><div class="relative mx-auto max-w-3xl"><p class="mb-4 text-xs font-black tracking-widest text-[#bfdbfe]">{{t.ctaEyebrow}}</p><h2 class="text-3xl leading-[1.45] font-black sm:text-5xl">{{t.ctaTitle}}</h2><p class="mx-auto mt-6 max-w-xl text-base leading-9 text-[#bfdbfe]">{{t.ctaDesc}}</p><div class="mt-9 flex flex-wrap items-center justify-center gap-3"><a v-if="waUrl" :href="waUrl" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 rounded-full bg-[#dbeafe] px-8 py-4 text-sm font-black text-[#102654] transition hover:bg-[#bfdbfe]"><MessageCircle :size="19"/>{{t.contactWhats}}<ArrowUpRight :size="17"/></a><a v-if="email" :href="'mailto:'+email" class="inline-flex items-center gap-2 rounded-full border border-white/30 px-7 py-4 text-sm font-black text-white transition hover:bg-white/10">{{t.contactMail}}<ArrowUpRight :size="17"/></a><p v-if="!waUrl&&!email" class="text-sm text-[#ced9e7]">{{t.contactNotSet}}</p></div></div></div></section>
  </main>
  <footer class="border-t border-[#e2e8f0] bg-white px-5 py-12 md:px-10"><div class="mx-auto grid max-w-[1400px] gap-8 md:grid-cols-3"><div><a href="#top" class="inline-flex items-center gap-2 font-black" @click="goTop"><GraduationCap :size="24" class="text-[#2563eb]"/><span dir="ltr">Sham<span class="text-[#2563eb]">.</span>Academy</span></a><p class="mt-3 max-w-xs text-sm leading-7 text-[#64748b]">{{t.footDesc}}</p></div><div><h4 class="mb-3 text-sm font-black">{{t.footQuick}}</h4><a v-for="item in nav.slice(0,3)" :key="item.id" :href="'#'+item.id" class="mb-2 block text-xs font-semibold text-[#5a6f94] hover:text-[#13408e]">{{item.label}}</a></div><div><h4 class="mb-3 text-sm font-black">{{t.contactUs}}</h4><a v-if="platformUrl" :href="platformUrl" class="mb-2 block text-xs font-bold text-[#1a3c78]">{{t.login}}</a><a v-if="email" :href="'mailto:'+email" class="block text-xs" dir="ltr">{{email}}</a><p class="mt-3 text-[11px] leading-6 text-[#94a3b8]">{{t.photoNote}}</p></div></div><div class="mx-auto mt-10 flex max-w-[1400px] flex-wrap justify-between gap-3 border-t border-[#e2e8f0] pt-6 text-xs text-[#94a3b8]"><span>© {{new Date().getFullYear()}} Sham Academy — {{t.copyright}}</span><span></span></div>  </footer>

  <!-- Floating WhatsApp Button -->
  <a
   
    :href="waUrl"
    target="_blank"
    rel="noopener noreferrer"
    aria-label="Chat with Sham Academy on WhatsApp"
    class="fixed bottom-6 end-6 z-[100] flex h-[64px] w-[64px] items-center justify-center rounded-full bg-[#25D366] text-white shadow-[0_8px_30px_rgba(37,211,102,0.4)] transition-all duration-300 hover:scale-110 hover:bg-[#20ba5a]"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 32 32"
      class="h-9 w-9"
      fill="currentColor"
    >
      <path d="M16 .8A15.1 15.1 0 0 0 3 23.5L1 31l7.7-2A15.2 15.2 0 1 0 16 .8Zm0 27.5a12.3 12.3 0 0 1-6.3-1.7l-.5-.3-4.5 1.2 1.2-4.4-.3-.5a12.4 12.4 0 1 1 10.4 5.7Zm6.8-9.2c-.4-.2-2.2-1.1-2.6-1.2-.3-.1-.6-.2-.8.2-.3.4-1 1.2-1.2 1.4-.2.2-.4.3-.8.1-.4-.2-1.6-.6-3.1-2-1.1-1-1.9-2.2-2.1-2.6-.2-.4 0-.6.2-.8l.6-.7c.2-.2.3-.4.4-.6.1-.2 0-.5 0-.7L12.2 9c-.3-.8-.6-.7-.8-.7h-.7c-.3 0-.7.1-1.1.5-.4.4-1.4 1.4-1.4 3.3s1.5 3.7 1.7 4c.2.3 2.9 4.4 7 6.1 1 .4 1.7.6 2.3.7 1 .3 1.9.2 2.6.2.8-.1 2.2-.9 2.5-1.8.3-.9.3-1.7.2-1.8-.1-.2-.4-.3-.8-.5Z"/>
    </svg>
  </a>

</div>
</template>
