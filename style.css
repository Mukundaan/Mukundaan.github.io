(function () {
  var sections = Array.prototype.slice.call(document.querySelectorAll('[data-hud-label]'));
  var total = sections.length;

  var navLinks = Array.prototype.slice.call(document.querySelectorAll('.nav-links a'));
  var hudBars = Array.prototype.slice.call(document.querySelectorAll('.hud-bars span'));
  var hudLabel = document.getElementById('hudLabel');
  var hudFrac = document.getElementById('hudFrac');
  var hudPct = document.getElementById('hudPct');
  var hudDbm = document.getElementById('hudDbm');

  var DBM_START = -95;
  var DBM_END = -50;

  function activeIndex() {
    var line = window.innerHeight * 0.35;
    var idx = 0;
    for (var i = 0; i < sections.length; i++) {
      var rect = sections[i].getBoundingClientRect();
      if (rect.top <= line) idx = i;
    }
    return idx;
  }

  function scrollPercent() {
    var max = document.documentElement.scrollHeight - window.innerHeight;
    if (max <= 0) return 0;
    return Math.min(100, Math.max(0, (window.scrollY / max) * 100));
  }

  function update() {
    var idx = activeIndex();
    var section = sections[idx];
    var label = section.getAttribute('data-hud-label');
    var id = section.id;

    if (hudLabel) hudLabel.textContent = label;
    if (hudFrac) hudFrac.textContent = (idx + 1) + '/' + total;

    var pct = scrollPercent();
    if (hudPct) hudPct.textContent = Math.round(pct) + '%';
    if (hudDbm) hudDbm.textContent = Math.round(DBM_START + (DBM_END - DBM_START) * (pct / 100)) + 'dBm';

    hudBars.forEach(function (bar, i) {
      var filled = i < Math.round(((idx + 1) / total) * hudBars.length);
      bar.classList.toggle('on', filled);
    });

    navLinks.forEach(function (link) {
      link.classList.toggle('active', link.dataset.nav === id);
    });
  }

  var ticking = false;
  window.addEventListener('scroll', function () {
    if (!ticking) {
      requestAnimationFrame(function () {
        update();
        ticking = false;
      });
      ticking = true;
    }
  });

  window.addEventListener('resize', update);
  update();
})();
