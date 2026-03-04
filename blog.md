---
layout: default
title: Blog Técnico AbsolutTI - Insights de Tecnologia em BH
description: Artigos técnicos sobre Cloud, Helpdesk e Monitoramento proativo para empresas.
permalink: /blog/
---

<style>
  .filter-btn {
    background-color: transparent;
    border: 2px solid #0d6efd;
    color: #0d6efd;
    padding: 8px 16px;
    border-radius: 50px;
    font-weight: 600;
    transition: all 0.3s ease;
    cursor: pointer;
    margin: 5px;
  }
  .filter-btn:hover, .filter-btn.active {
    background-color: #0d6efd;
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(13, 110, 253, 0.2);
  }
</style>

<div style="max-width: 800px; margin: 0 auto; padding: 20px;">
  <h1 style="color: #0d6efd; border-bottom: 2px solid #0d6efd; padding-bottom: 10px;">Insights de Tecnologia</h1>
  
  <div style="margin: 30px 0; text-align: center;">
    <p style="margin-bottom: 15px; font-weight: bold; color: #555;">Filtrar por Especialidade:</p>
    <button onclick="filterCategory('all', this)" class="filter-btn active" id="btn-all">Tudo</button>
    <button onclick="filterCategory('Cloud', this)" class="filter-btn" id="btn-Cloud">Cloud</button>
    <button onclick="filterCategory('Helpdesk', this)" class="filter-btn" id="btn-Helpdesk">Helpdesk</button>
    <button onclick="filterCategory('Tutoriais', this)" class="filter-btn" id="btn-Tutoriais">Tutoriais</button>
  </div>

  <div id="post-container">
  {% for post in site.posts %}
    <article class="post-item" data-category="{{ post.categories | join: ',' }}" style="margin-bottom: 40px; background: #fff; padding: 25px; border-radius: 12px; border: 1px solid #eee; transition: 0.3s;">
      <h2 style="margin-bottom: 8px;">
        <a href="{{ post.url }}" style="text-decoration: none; color: #212529;">{{ post.title }}</a>
      </h2>
      <small style="color: #6c757d; display: block; margin-bottom: 15px;">
        <i class="bi bi-calendar"></i> {{ post.date | date: "%d/%m/%Y" }} | <strong>Categoria:</strong> {{ post.categories | join: ", " }}
      </small>
      <p style="color: #444; line-height: 1.6;">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      <a href="{{ post.url }}" style="color: #0d6efd; font-weight: bold; text-decoration: none; display: inline-flex; align-items: center; gap: 5px;">
        Ler Artigo Completo <i class="bi bi-arrow-right"></i>
      </a>
    </article>
  {% endfor %}
  </div>
</div>

<script>
function filterCategory(category, btn) {
  // Atualiza botões
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  if (btn) {
    btn.classList.add('active');
  } else {
    const targetBtn = document.getElementById('btn-' + category);
    if (targetBtn) targetBtn.classList.add('active');
  }

  // Filtra posts
  const posts = document.querySelectorAll('.post-item');
  posts.forEach(post => {
    const categories = post.getAttribute('data-category');
    if (category === 'all' || categories.includes(category)) {
      post.style.display = 'block';
    } else {
      post.style.display = 'none';
    }
  });
}

// Lógica para filtrar automaticamente via URL (ex: ?cat=Cloud)
window.addEventListener('DOMContentLoaded', () => {
  const params = new URLSearchParams(window.location.search);
  const cat = params.get('cat');
  if (cat) {
    filterCategory(cat);
  }
});
</script>