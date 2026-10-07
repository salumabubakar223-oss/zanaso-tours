const STORAGE_KEY = 'zanaso_site_data';

const defaultData = {
  brandName: 'ZANASO',
  logoUrl: 'https://images.unsplash.com/photo-1523906834658-6e24ef2386f9?auto=format&fit=crop&w=300&q=80',
  hero: {
    eyebrow: 'Discover Zanzibar',
    title: 'Welcome to ZANASO',
    description:
      'Your Zanzibar Adventure Starts Here. From Stone Town to turquoise waters, tropical beaches and unforgettable wildlife safaris, we create journeys designed to make your holiday special.',
    primaryButton: 'Explore Tours',
    secondaryButton: 'Book Your Adventure',
    backgroundImage:
      'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1600&q=80'
  },
  features: [
    {
      icon: '🏝️',
      title: 'Zanzibar Excursions',
      text: 'Discover beaches, islands, caves, forests and local villages in the most beautiful corners of Zanzibar.'
    },
    {
      icon: '🤿',
      title: 'Ocean Adventures',
      text: 'Swim, snorkel and explore crystal-clear waters with unforgettable marine life experiences.'
    },
    {
      icon: '🦁',
      title: 'Tanzania Safaris',
      text: 'Experience Africa’s wildlife with memorable safaris through iconic national parks.'
    },
    {
      icon: '🚕',
      title: 'Airport & Hotel Transfers',
      text: 'Enjoy safe, comfortable and reliable transport from the airport, ferry terminal or accommodation.'
    }
  ],
  tours: [
    {
      title: 'Stone Town Experience',
      description: 'Walk through the historic heart of Zanzibar, discover its culture, markets and fascinating history.',
      price: 'From $XX',
      image: 'https://images.unsplash.com/photo-1500375592092-40eb2168fd21?auto=format&fit=crop&w=900&q=80'
    },
    {
      title: 'Blue Lagoon & Michamvi',
      description: 'Enjoy crystal-clear water, snorkeling, beautiful beaches and a relaxing island experience.',
      price: 'From $XX',
      image: 'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=900&q=80'
    },
    {
      title: 'Jozani Forest',
      description: 'Discover Zanzibar’s famous red colobus monkeys and explore the beautiful tropical forest.',
      price: 'From $XX',
      image: 'https://images.unsplash.com/photo-1473448912268-2022ce9509d8?auto=format&fit=crop&w=900&q=80'
    },
    {
      title: 'Prison Island',
      description: 'Visit the historic island, see giant Aldabra tortoises and enjoy beautiful ocean views.',
      price: 'From $XX',
      image: 'https://images.unsplash.com/photo-1501785888041-af3ef285b470?auto=format&fit=crop&w=900&q=80'
    }
  ],
  why: [
    { icon: '📍', title: 'Local Experts', text: 'We know Zanzibar and understand what makes a great travel experience.' },
    { icon: '🤝', title: 'Personal Service', text: 'We listen to what you want and help create the perfect trip for you.' },
    { icon: '🚐', title: 'Reliable & Comfortable', text: 'From airport pickup to your final excursion, safety and comfort come first.' },
    { icon: '🌍', title: 'Flexible Experiences', text: 'Travel solo, as a couple, with family or friends; we adapt to your needs.' },
    { icon: '💬', title: 'Great Memories', text: 'Our goal is simple: to make every Zanzibar journey unforgettable.' },
    { icon: '✅', title: 'Trusted Planning', text: 'We organize your experience with care, efficiency and attention to detail.' }
  ],
  testimonials: [
    {
      quote: 'An amazing experience from beginning to end. Everything was well organized and our guide was friendly and helpful.',
      author: 'Happy Guest'
    },
    {
      quote: 'Zanzibar was beautiful, but the ZANASO team made our trip even more special.',
      author: 'Happy Guest'
    },
    {
      quote: 'Professional, friendly and reliable. We would definitely book again.',
      author: 'Happy Guest'
    }
  ],
  contact: {
    location: 'Zanzibar, Tanzania',
    whatsapp: '+255 XXX XXX XXX',
    email: 'info@zan...com',
    website: 'www.zanaso.com',
    instagram: 'Instagram',
    facebook: 'Facebook',
    tiktok: 'TikTok',
    youtube: 'YouTube'
  },
  booking: {
    title: 'Book Your Zanzibar Adventure',
    description: 'Tell us what you would like to experience and our team will help you plan the perfect trip.',
    options: ['Zanzibar Excursion', 'Safari', 'Airport Transfer', 'Beach Experience', 'Ocean Adventure', 'Private Tour', 'Other']
  }
};

function getStoredData() {
  const stored = localStorage.getItem(STORAGE_KEY);
  if (!stored) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(defaultData));
    return structuredClone(defaultData);
  }

  try {
    return { ...structuredClone(defaultData), ...JSON.parse(stored) };
  } catch (error) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(defaultData));
    return structuredClone(defaultData);
  }
}

function saveData(data) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
}

function escapeHtml(value) {
  return String(value)
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#039;');
}

function renderHomePage() {
  const siteData = getStoredData();

  document.getElementById('brandName').textContent = siteData.brandName || 'ZANASO';
  const logoEl = document.getElementById('siteLogo');
  if (logoEl) {
    logoEl.src = siteData.logoUrl || defaultData.logoUrl;
    logoEl.alt = `${siteData.brandName || 'ZANASO'} Logo`;
  }

  const heroSection = document.getElementById('heroSection');
  if (heroSection) {
    heroSection.style.backgroundImage = `url(${siteData.hero.backgroundImage || defaultData.hero.backgroundImage})`;
  }

  const heroEyebrow = document.getElementById('heroEyebrow');
  if (heroEyebrow) heroEyebrow.textContent = siteData.hero.eyebrow || defaultData.hero.eyebrow;

  const heroTitle = document.getElementById('heroTitle');
  if (heroTitle) heroTitle.textContent = siteData.hero.title || defaultData.hero.title;

  const heroDescription = document.getElementById('heroDescription');
  if (heroDescription) heroDescription.textContent = siteData.hero.description || defaultData.hero.description;

  const heroPrimaryBtn = document.getElementById('heroPrimaryBtn');
  const heroSecondaryBtn = document.getElementById('heroSecondaryBtn');
  if (heroPrimaryBtn) heroPrimaryBtn.textContent = siteData.hero.primaryButton || defaultData.hero.primaryButton;
  if (heroSecondaryBtn) heroSecondaryBtn.textContent = siteData.hero.secondaryButton || defaultData.hero.secondaryButton;

  const featuresGrid = document.getElementById('featuresGrid');
  if (featuresGrid) {
    featuresGrid.innerHTML = (siteData.features || defaultData.features)
      .map(
        (item) => `
          <article class="feature">
            <div class="icon">${escapeHtml(item.icon || '★')}</div>
            <h3>${escapeHtml(item.title || '')}</h3>
            <p>${escapeHtml(item.text || '')}</p>
          </article>
        `
      )
      .join('');
  }

  const toursGrid = document.getElementById('toursGrid');
  if (toursGrid) {
    toursGrid.innerHTML = (siteData.tours || defaultData.tours)
      .map(
        (tour) => `
          <article class="tour-card">
            <img src="${escapeHtml(tour.image || '')}" alt="${escapeHtml(tour.title || '')}" />
            <div class="tour-body">
              <h3>${escapeHtml(tour.title || '')}</h3>
              <p>${escapeHtml(tour.description || '')}</p>
              <div class="tour-meta">
                <span class="price">${escapeHtml(tour.price || 'From $XX')}</span>
                <a class="btn btn-primary" href="#booking">Book Now</a>
              </div>
            </div>
          </article>
        `
      )
      .join('');
  }

  const whyGrid = document.getElementById('whyGrid');
  if (whyGrid) {
    whyGrid.innerHTML = (siteData.why || defaultData.why)
      .map(
        (item) => `
          <div class="why-item">
            <div class="why-icon">${escapeHtml(item.icon || '✓')}</div>
            <div>
              <h4>${escapeHtml(item.title || '')}</h4>
              <p>${escapeHtml(item.text || '')}</p>
            </div>
          </div>
        `
      )
      .join('');
  }

  const testimonialsGrid = document.getElementById('testimonialsGrid');
  if (testimonialsGrid) {
    testimonialsGrid.innerHTML = (siteData.testimonials || defaultData.testimonials)
      .map(
        (item) => `
          <article class="quote">
            <p>“${escapeHtml(item.quote || '')}”</p>
            <strong>— ${escapeHtml(item.author || 'Happy Guest')}</strong>
          </article>
        `
      )
      .join('');
  }

  const bookingTitle = document.getElementById('bookingTitle');
  const bookingDescription = document.getElementById('bookingDescription');
  const bookingList = document.getElementById('bookingList');
  if (bookingTitle) bookingTitle.textContent = siteData.booking.title || defaultData.booking.title;
  if (bookingDescription) bookingDescription.textContent = siteData.booking.description || defaultData.booking.description;
  if (bookingList) {
    const options = siteData.booking.options || defaultData.booking.options;
    bookingList.innerHTML = options.map((value) => `<li>${escapeHtml(value)}</li>`).join('');
  }

  const experienceSelect = document.getElementById('experience');
  if (experienceSelect) {
    experienceSelect.innerHTML = (siteData.booking.options || defaultData.booking.options)
      .map((value) => `<option>${escapeHtml(value)}</option>`)
      .join('');
  }

  const footerBrand = document.getElementById('footerBrand');
  const footerLocation = document.getElementById('footerLocation');
  const footerWhatsApp = document.getElementById('footerWhatsApp');
  const footerEmail = document.getElementById('footerEmail');
  const footerWebsite = document.getElementById('footerWebsite');
  const socialLinks = document.getElementById('socialLinks');

  if (footerBrand) footerBrand.textContent = siteData.brandName || 'ZANASO';
  if (footerLocation) footerLocation.textContent = `📍 ${siteData.contact.location || defaultData.contact.location}`;
  if (footerWhatsApp) footerWhatsApp.textContent = `📱 WhatsApp: ${siteData.contact.whatsapp || defaultData.contact.whatsapp}`;
  if (footerEmail) footerEmail.textContent = `📧 Email: ${siteData.contact.email || defaultData.contact.email}`;
  if (footerWebsite) footerWebsite.textContent = `🌐 Website: ${siteData.contact.website || defaultData.contact.website}`;

  if (socialLinks) {
    const links = [
      { label: siteData.contact.instagram || 'Instagram', href: '#' },
      { label: siteData.contact.facebook || 'Facebook', href: '#' },
      { label: siteData.contact.tiktok || 'TikTok', href: '#' },
      { label: siteData.contact.youtube || 'YouTube', href: '#' }
    ];

    socialLinks.innerHTML = links.map((link) => `<a href="${escapeHtml(link.href)}">${escapeHtml(link.label)}</a>`).join('');
  }
}

function getTextInput(id, fallback) {
  const el = document.getElementById(id);
  return el ? (el.value || fallback) : fallback;
}

function createFeatureEditor(features) {
  const container = document.getElementById('featureEditor');
  if (!container) return;

  container.innerHTML = features.map(
    (feature, index) => `
      <div class="editor-item">
        <h3>Feature ${index + 1}</h3>
        <div class="admin-grid">
          <div class="field">
            <label>Icon</label>
            <input data-feature-index="${index}" data-field="icon" value="${escapeHtml(feature.icon || '')}" />
          </div>
          <div class="field">
            <label>Title</label>
            <input data-feature-index="${index}" data-field="title" value="${escapeHtml(feature.title || '')}" />
          </div>
          <div class="field full">
            <label>Text</label>
            <textarea data-feature-index="${index}" data-field="text">${escapeHtml(feature.text || '')}</textarea>
          </div>
        </div>
      </div>
    `
  ).join('');
}

function createTourEditor(tours) {
  const container = document.getElementById('tourEditor');
  if (!container) return;

  container.innerHTML = tours.map(
    (tour, index) => `
      <div class="editor-item">
        <h3>Tour ${index + 1}</h3>
        <div class="admin-grid">
          <div class="field">
            <label>Title</label>
            <input data-tour-index="${index}" data-field="title" value="${escapeHtml(tour.title || '')}" />
          </div>
          <div class="field">
            <label>Price</label>
            <input data-tour-index="${index}" data-field="price" value="${escapeHtml(tour.price || '')}" />
          </div>
          <div class="field full">
            <label>Description</label>
            <textarea data-tour-index="${index}" data-field="description">${escapeHtml(tour.description || '')}</textarea>
          </div>
          <div class="field full">
            <label>Image URL</label>
            <input data-tour-index="${index}" data-field="image" value="${escapeHtml(tour.image || '')}" />
          </div>
        </div>
      </div>
    `
  ).join('');
}

function createWhyEditor(items) {
  const container = document.getElementById('whyEditor');
  if (!container) return;

  container.innerHTML = items.map(
    (item, index) => `
      <div class="editor-item">
        <h3>Item ${index + 1}</h3>
        <div class="admin-grid">
          <div class="field">
            <label>Icon</label>
            <input data-why-index="${index}" data-field="icon" value="${escapeHtml(item.icon || '')}" />
          </div>
          <div class="field">
            <label>Title</label>
            <input data-why-index="${index}" data-field="title" value="${escapeHtml(item.title || '')}" />
          </div>
          <div class="field full">
            <label>Text</label>
            <textarea data-why-index="${index}" data-field="text">${escapeHtml(item.text || '')}</textarea>
          </div>
        </div>
      </div>
    `
  ).join('');
}

function createTestimonialEditor(items) {
  const container = document.getElementById('testimonialEditor');
  if (!container) return;

  container.innerHTML = items.map(
    (item, index) => `
      <div class="editor-item">
        <h3>Testimonial ${index + 1}</h3>
        <div class="admin-grid">
          <div class="field full">
            <label>Quote</label>
            <textarea data-testimonial-index="${index}" data-field="quote">${escapeHtml(item.quote || '')}</textarea>
          </div>
          <div class="field full">
            <label>Author</label>
            <input data-testimonial-index="${index}" data-field="author" value="${escapeHtml(item.author || '')}" />
          </div>
        </div>
      </div>
    `
  ).join('');
}

function populateAdminForm() {
  const siteData = getStoredData();

  document.getElementById('brandNameInput').value = siteData.brandName || 'ZANASO';
  document.getElementById('logoUrlInput').value = siteData.logoUrl || defaultData.logoUrl;
  document.getElementById('heroImageInput').value = siteData.hero.backgroundImage || defaultData.hero.backgroundImage;
  document.getElementById('heroEyebrowInput').value = siteData.hero.eyebrow || defaultData.hero.eyebrow;
  document.getElementById('heroTitleInput').value = siteData.hero.title || defaultData.hero.title;
  document.getElementById('heroDescriptionInput').value = siteData.hero.description || defaultData.hero.description;
  document.getElementById('heroPrimaryBtnInput').value = siteData.hero.primaryButton || defaultData.hero.primaryButton;
  document.getElementById('heroSecondaryBtnInput').value = siteData.hero.secondaryButton || defaultData.hero.secondaryButton;

  document.getElementById('locationInput').value = siteData.contact.location || defaultData.contact.location;
  document.getElementById('phoneInput').value = siteData.contact.whatsapp || defaultData.contact.whatsapp;
  document.getElementById('emailInput').value = siteData.contact.email || defaultData.contact.email;
  document.getElementById('websiteInput').value = siteData.contact.website || defaultData.contact.website;
  document.getElementById('instagramInput').value = siteData.contact.instagram || defaultData.contact.instagram;
  document.getElementById('facebookInput').value = siteData.contact.facebook || defaultData.contact.facebook;
  document.getElementById('tiktokInput').value = siteData.contact.tiktok || defaultData.contact.tiktok;
  document.getElementById('youtubeInput').value = siteData.contact.youtube || defaultData.contact.youtube;

  createFeatureEditor(siteData.features || defaultData.features);
  createTourEditor(siteData.tours || defaultData.tours);
  createWhyEditor(siteData.why || defaultData.why);
  createTestimonialEditor(siteData.testimonials || defaultData.testimonials);
}

function collectAdminData() {
  const siteData = getStoredData();

  siteData.brandName = getTextInput('brandNameInput', defaultData.brandName);
  siteData.logoUrl = getTextInput('logoUrlInput', defaultData.logoUrl);
  siteData.hero.eyebrow = getTextInput('heroEyebrowInput', defaultData.hero.eyebrow);
  siteData.hero.title = getTextInput('heroTitleInput', defaultData.hero.title);
  siteData.hero.description = getTextInput('heroDescriptionInput', defaultData.hero.description);
  siteData.hero.primaryButton = getTextInput('heroPrimaryBtnInput', defaultData.hero.primaryButton);
  siteData.hero.secondaryButton = getTextInput('heroSecondaryBtnInput', defaultData.hero.secondaryButton);
  siteData.hero.backgroundImage = getTextInput('heroImageInput', defaultData.hero.backgroundImage);

  siteData.features = Array.from(document.querySelectorAll('[data-feature-index]')).reduce((acc, input) => {
    const index = Number(input.dataset.featureIndex);
    const field = input.dataset.field;
    if (!acc[index]) acc[index] = {};
    acc[index][field] = input.value;
    return acc;
  }, []);

  siteData.tours = Array.from(document.querySelectorAll('[data-tour-index]')).reduce((acc, input) => {
    const index = Number(input.dataset.tourIndex);
    const field = input.dataset.field;
    if (!acc[index]) acc[index] = {};
    acc[index][field] = input.value;
    return acc;
  }, []);

  siteData.why = Array.from(document.querySelectorAll('[data-why-index]')).reduce((acc, input) => {
    const index = Number(input.dataset.whyIndex);
    const field = input.dataset.field;
    if (!acc[index]) acc[index] = {};
    acc[index][field] = input.value;
    return acc;
  }, []);

  siteData.testimonials = Array.from(document.querySelectorAll('[data-testimonial-index]')).reduce((acc, input) => {
    const index = Number(input.dataset.testimonialIndex);
    const field = input.dataset.field;
    if (!acc[index]) acc[index] = {};
    acc[index][field] = input.value;
    return acc;
  }, []);

  siteData.contact.location = getTextInput('locationInput', defaultData.contact.location);
  siteData.contact.whatsapp = getTextInput('phoneInput', defaultData.contact.whatsapp);
  siteData.contact.email = getTextInput('emailInput', defaultData.contact.email);
  siteData.contact.website = getTextInput('websiteInput', defaultData.contact.website);
  siteData.contact.instagram = getTextInput('instagramInput', defaultData.contact.instagram);
  siteData.contact.facebook = getTextInput('facebookInput', defaultData.contact.facebook);
  siteData.contact.tiktok = getTextInput('tiktokInput', defaultData.contact.tiktok);
  siteData.contact.youtube = getTextInput('youtubeInput', defaultData.contact.youtube);

  return siteData;
}

function saveChanges() {
  const siteData = collectAdminData();
  saveData(siteData);
  renderHomePage();
  alert('Changes saved successfully.');
}

function resetDemoData() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(defaultData));
  populateAdminForm();
  renderHomePage();
  alert('Demo data restored.');
}

document.addEventListener('DOMContentLoaded', () => {
  if (document.getElementById('saveButton')) {
    document.getElementById('saveButton').addEventListener('click', saveChanges);
  }

  if (document.getElementById('resetButton')) {
    document.getElementById('resetButton').addEventListener('click', resetDemoData);
  }

  if (document.getElementById('heroSection') || document.getElementById('featuresGrid')) {
    renderHomePage();
  }

  if (document.getElementById('brandNameInput')) {
    populateAdminForm();
  }
});

window.zanaso = {
  defaultData,
  getStoredData,
  saveData,
  renderHomePage,
  saveChanges,
  resetDemoData
};
