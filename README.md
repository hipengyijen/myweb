<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>行動支付的資安風險與防護對策</title>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    :root {
      --primary: #2563eb;
      --primary-dark: #1d4ed8;
      --secondary: #64748b;
      --accent: #f59e0b;
      --accent-light: #fcd34d;
      --highlight: #fef3c7;
      --highlight-text: #92400e;
      --background: #f8fafc;
      --text: #1e293b;
      --card-bg: #ffffff;
      --border: #e2e8f0;
      --gradient-start: #3b82f6;
      --gradient-end: #1d4ed8;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Noto Sans TC', sans-serif;
      background: var(--background);
      color: var(--text);
      line-height: 1.8;
    }

    header {
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      color: white;
      padding: 6rem 2rem;
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .hero-content {
      max-width: 1200px;
      margin: 0 auto;
      position: relative;
      z-index: 2;
      padding: 2rem;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 2rem;
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.2);
    }

    .hero-title {
      font-size: 4rem;
      margin-bottom: 2rem;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
      animation: fadeInUp 1s ease-out;
      background: linear-gradient(45deg, #fff, var(--accent-light));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      font-weight: 700;
      letter-spacing: 2px;
    }

    .hero-subtitle {
      font-size: 1.8rem;
      margin-bottom: 3rem;
      opacity: 0.9;
      animation: fadeInUp 1s ease-out 0.3s;
      animation-fill-mode: both;
      color: rgba(255, 255, 255, 0.95);
      text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
      letter-spacing: 1px;
    }

    .hero-image {
      width: 100%;
      max-width: 800px;
      margin: 2rem auto;
      border-radius: 1rem;
      box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04);
      transition: transform 0.3s ease;
    }

    .hero-image:hover {
      transform: translateY(-5px);
    }

    main {
      max-width: 1200px;
      margin: 2rem auto;
      padding: 0 2rem;
    }

    nav {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      padding: 1.5rem;
      border-radius: 1.5rem;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      margin: -3rem auto 2rem;
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      justify-content: center;
      position: sticky;
      top: 1rem;
      z-index: 100;
      max-width: 1200px;
    }

    nav button {
      padding: 1.2rem 2rem;
      background: transparent;
      color: var(--text);
      border: 2px solid var(--border);
      border-radius: 1.5rem;
      cursor: pointer;
      font-weight: 500;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 0.8rem;
      font-size: 1rem;
      letter-spacing: 0.5px;
    }

    nav button i {
      font-size: 1.4rem;
      transition: transform 0.3s ease;
    }

    nav button:hover {
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      color: white;
      border-color: transparent;
      transform: translateY(-3px);
      box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3);
    }

    nav button:hover i {
      transform: scale(1.2);
    }

    nav button.active {
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      color: white;
      border-color: transparent;
      box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3);
    }

    .section-header {
      text-align: center;
      margin-bottom: 3rem;
    }

    .section-header img {
      width: 100%;
      max-width: 800px;
      border-radius: 1.5rem;
      margin-bottom: 2rem;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    }

    .image-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin: 2rem 0;
    }

    .image-card {
      position: relative;
      overflow: hidden;
      border-radius: 1rem;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }

    .image-card:hover {
      transform: translateY(-5px);
    }

    .image-card img {
      width: 100%;
      height: 250px;
      object-fit: cover;
    }

    .image-card .card-content {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 1.5rem;
      background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
      color: white;
    }

    .image-card .card-content h3 {
      font-size: 1.2rem;
      margin-bottom: 0.5rem;
    }

    .floating-image {
      position: absolute;
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 50%;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      animation: float 6s ease-in-out infinite;
    }

    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
      100% { transform: translateY(0px); }
    }

    .section-content {
      position: relative;
      padding: 2rem;
    }

    .floating-image-1 {
      top: 10%;
      right: 5%;
    }

    .floating-image-2 {
      bottom: 15%;
      left: 5%;
    }

    @media (max-width: 768px) {
      .hero-title {
        font-size: 3rem;
      }

      .hero-subtitle {
        font-size: 1.5rem;
      }

      .card {
        padding: 2rem;
      }

      .gallery-item {
        height: 250px;
      }

      nav button {
        padding: 1rem 1.5rem;
        font-size: 0.9rem;
      }
    }

    section {
      display: none;
      opacity: 0;
      transform: translateY(20px);
      transition: all 0.4s ease;
    }

    section.active {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }

    .section-content {
      max-width: 1000px;
      margin: 0 auto;
      padding: 2rem;
    }

    h2 {
      color: var(--primary);
      margin-bottom: 2rem;
      font-size: 2rem;
      padding-bottom: 1rem;
      position: relative;
      text-align: center;
      background: linear-gradient(120deg, var(--gradient-start), var(--gradient-end));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      display: inline-block;
      width: 100%;
    }

    h2::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 100px;
      height: 3px;
      background: linear-gradient(90deg, var(--gradient-start), var(--gradient-end));
      border-radius: 3px;
    }

    .highlight {
      background-color: var(--highlight);
      color: var(--highlight-text);
      padding: 0.2em 0.4em;
      border-radius: 0.3em;
      font-weight: 500;
    }

    .card {
      background: var(--card-bg);
      padding: 3rem;
      border-radius: 2rem;
      box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04);
      margin-bottom: 3rem;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 4px;
      background: linear-gradient(90deg, var(--gradient-start), var(--gradient-end));
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 25px 30px -5px rgba(0,0,0,0.15);
    }

    .grid-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin: 2rem 0;
    }

    .feature-item {
      background: white;
      padding: 2.5rem;
      border-radius: 1.5rem;
      box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      overflow: hidden;
    }

    .feature-item:hover {
      transform: translateY(-5px);
      box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1);
    }

    .feature-icon {
      font-size: 2.5rem;
      background: linear-gradient(135deg, var(--primary), var(--accent));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 1.5rem;
      text-align: center;
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0% {
        transform: scale(1);
      }
      50% {
        transform: scale(1.1);
      }
      100% {
        transform: scale(1);
      }
    }

    .feature-title {
      font-size: 1.5rem;
      color: var(--text);
      margin-bottom: 1.5rem;
      font-weight: 600;
      position: relative;
      padding-left: 2rem;
      display: inline-block;
      transition: transform 0.3s ease;
    }

    .feature-title::before {
      content: '🔸';
      position: absolute;
      left: 0;
      top: 50%;
      transform: translateY(-50%);
      font-size: 1.2rem;
    }

    .feature-title:hover {
      transform: translateX(10px);
    }

    .security-tip {
      background: linear-gradient(135deg, #f0f9ff 0%, #e6f3ff 100%);
      border-left: 4px solid var(--primary);
      padding: 1.5rem;
      margin: 1.5rem 0;
      border-radius: 0.75rem;
      box-shadow: 0 4px 6px rgba(0,0,0,0.05);
      position: relative;
      overflow: hidden;
    }

    .security-tip::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(45deg, transparent, rgba(255,255,255,0.8), transparent);
      transform: translateX(-100%);
      animation: shine 3s infinite;
    }

    @keyframes shine {
      0% {
        transform: translateX(-100%);
      }
      20% {
        transform: translateX(100%);
      }
      100% {
        transform: translateX(100%);
      }
    }

    .image-gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2.5rem;
      margin: 3rem 0;
    }

    .gallery-item {
      position: relative;
      border-radius: 1.5rem;
      overflow: hidden;
      box-shadow: 0 15px 25px -5px rgba(0,0,0,0.2);
      transition: transform 0.3s ease;
    }

    .gallery-item img {
      width: 100%;
      height: 300px;
      object-fit: cover;
      transition: transform 0.5s ease;
    }

    .gallery-item:hover {
      transform: translateY(-10px);
    }

    .gallery-item:hover img {
      transform: scale(1.1);
    }

    .gallery-caption {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 2rem;
      background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
      color: white;
      transform: translateY(100%);
      transition: transform 0.3s ease;
    }

    .gallery-item:hover .gallery-caption {
      transform: translateY(0);
    }

    footer {
      background: var(--text);
      color: white;
      text-align: center;
      padding: 3rem 2rem;
      margin-top: 4rem;
    }

    .footer-content {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
    }

    .footer-section {
      text-align: left;
    }

    .footer-section h3 {
      margin-bottom: 1rem;
      color: var(--accent);
    }

    .footer-section ul {
      list-style: none;
    }

    .footer-section ul li {
      margin-bottom: 0.5rem;
    }

    .footer-section a {
      color: white;
      text-decoration: none;
      transition: color 0.3s ease;
    }

    .footer-section a:hover {
      color: var(--accent);
    }

    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .feature-image {
      width: 100%;
      max-width: 800px;
      height: auto;
      border-radius: 1.5rem;
      margin: 2rem auto;
      display: block;
      box-shadow: 0 15px 30px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }

    .feature-image:hover {
      transform: translateY(-10px);
    }

    .image-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin: 2rem 0;
    }

    .image-card {
      position: relative;
      border-radius: 1.5rem;
      overflow: hidden;
      box-shadow: 0 15px 30px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }

    .image-card:hover {
      transform: translateY(-10px);
    }

    .image-card img {
      width: 100%;
      height: 250px;
      object-fit: cover;
      transition: transform 0.5s ease;
    }

    .image-card:hover img {
      transform: scale(1.1);
    }

    .card-content {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 2rem;
      background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
      color: white;
      transform: translateY(100%);
      transition: transform 0.3s ease;
    }

    .image-card:hover .card-content {
      transform: translateY(0);
    }

    .image-showcase {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2.5rem;
      margin: 3rem 0;
    }

    .showcase-item {
      position: relative;
      border-radius: 1.5rem;
      overflow: hidden;
      box-shadow: 0 15px 30px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }

    .showcase-item:hover {
      transform: translateY(-10px);
    }

    .showcase-item img {
      width: 100%;
      height: 300px;
      object-fit: cover;
      transition: transform 0.5s ease;
    }

    .showcase-item:hover img {
      transform: scale(1.1);
    }

    .showcase-content {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 2rem;
      background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
      color: white;
      transform: translateY(100%);
      transition: transform 0.3s ease;
    }

    .showcase-item:hover .showcase-content {
      transform: translateY(0);
    }

    @media (max-width: 768px) {
      .image-card, .showcase-item {
        height: 200px;
      }

      .feature-image {
        margin: 1.5rem auto;
      }

      .image-grid, .image-showcase {
        gap: 1.5rem;
      }
    }

    /* 新增圖標卡片樣式 */
    .icon-card {
      background: white;
      padding: 2rem;
      border-radius: 1.5rem;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      text-align: center;
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    .icon-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      opacity: 0;
      transition: opacity 0.3s ease;
      z-index: 1;
    }

    .icon-card:hover::before {
      opacity: 0.1;
    }

    .icon-card i {
      font-size: 3rem;
      margin-bottom: 1.5rem;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      transition: transform 0.3s ease;
    }

    .icon-card:hover i {
      transform: scale(1.2);
    }

    .icon-card h3 {
      margin-bottom: 1rem;
      font-size: 1.5rem;
      color: var(--text);
    }

    .icon-card p {
      color: var(--secondary);
      line-height: 1.6;
    }

    /* 新增統計數字樣式 */
    .stats-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 2rem;
      margin: 3rem 0;
    }

    .stat-item {
      text-align: center;
      padding: 2rem;
      background: white;
      border-radius: 1.5rem;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }

    .stat-item:hover {
      transform: translateY(-5px);
    }

    .stat-number {
      font-size: 3rem;
      font-weight: 700;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 1rem;
    }

    .stat-label {
      color: var(--secondary);
      font-size: 1.1rem;
    }

    /* 更新區塊標題樣式 */
    .section-title {
      text-align: center;
      margin-bottom: 3rem;
      position: relative;
    }

    .section-title h2 {
      font-size: 2.5rem;
      margin-bottom: 1rem;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .section-title p {
      color: var(--secondary);
      font-size: 1.2rem;
      max-width: 600px;
      margin: 0 auto;
    }

    /* 更新內容區塊樣式 */
    .content-block {
      background: white;
      padding: 3rem;
      border-radius: 2rem;
      box-shadow: 0 15px 30px rgba(0,0,0,0.1);
      margin-bottom: 3rem;
    }

    .content-block h3 {
      font-size: 1.8rem;
      margin-bottom: 2rem;
      color: var(--text);
    }

    /* 更新列表樣式 */
    .feature-list {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
      margin: 2rem 0;
    }

    .feature-list-item {
      display: flex;
      align-items: flex-start;
      gap: 1rem;
      padding: 1.5rem;
      background: rgba(255,255,255,0.5);
      border-radius: 1rem;
      transition: transform 0.3s ease;
    }

    .feature-list-item:hover {
      transform: translateX(10px);
    }

    .feature-list-item i {
      font-size: 1.5rem;
      color: var(--primary);
    }

    .feature-list-item div h4 {
      margin: 0 0 0.5rem 0;
      color: var(--text);
    }

    .feature-list-item div p {
      margin: 0;
      color: var(--secondary);
      font-size: 0.95rem;
    }

    /* 更新警告框樣式 */
    .alert-box {
      background: linear-gradient(135deg, #fff5f5 0%, #ffe4e4 100%);
      border-left: 4px solid #dc2626;
      padding: 2rem;
      border-radius: 1rem;
      margin: 2rem 0;
      position: relative;
      overflow: hidden;
    }

    .alert-box::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(45deg, transparent, rgba(255,255,255,0.8), transparent);
      transform: translateX(-100%);
      animation: shine 3s infinite;
    }

    .alert-box h4 {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      color: #dc2626;
      margin-bottom: 1rem;
    }

    .alert-box h4 i {
      font-size: 1.5rem;
    }

    /* 更新響應式設計 */
    @media (max-width: 768px) {
      .icon-card {
        padding: 1.5rem;
      }

      .icon-card i {
        font-size: 2.5rem;
      }

      .stat-item {
        padding: 1.5rem;
      }

      .stat-number {
        font-size: 2.5rem;
      }

      .content-block {
        padding: 2rem;
      }

      .feature-list-item {
        padding: 1rem;
      }
    }

    /* 新增表格樣式 */
    .comparison-table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      margin: 2rem 0;
      background: white;
      border-radius: 1rem;
      overflow: hidden;
      box-shadow: 0 0 20px rgba(0,0,0,0.1);
    }

    .comparison-table th,
    .comparison-table td {
      padding: 1.5rem;
      text-align: left;
      border-bottom: 1px solid var(--border);
    }

    .comparison-table th {
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      color: white;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 1px;
      font-size: 0.9rem;
    }

    .comparison-table tr:last-child td {
      border-bottom: none;
    }

    .comparison-table td {
      transition: all 0.3s ease;
    }

    .comparison-table tr:hover td {
      background-color: rgba(37, 99, 235, 0.05);
    }

    .comparison-table .highlight {
      background: var(--highlight);
      color: var(--highlight-text);
      padding: 0.2rem 0.5rem;
      border-radius: 0.3rem;
      font-weight: 500;
      display: inline-block;
      margin: 0.2rem 0;
    }

    .comparison-table .advantage {
      color: #059669;
    }

    .comparison-table .disadvantage {
      color: #dc2626;
    }

    .comparison-table i {
      margin-right: 0.5rem;
    }

    /* 表格響應式設計 */
    @media (max-width: 768px) {
      .comparison-table {
        display: block;
        overflow-x: auto;
        white-space: nowrap;
      }
    }

    /* 應變處理樣式 */
    .emergency-flow {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin: 2rem 0;
    }

    .emergency-step {
      background: white;
      padding: 2rem;
      border-radius: 1rem;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      position: relative;
      overflow: hidden;
      transition: transform 0.3s ease;
    }

    .emergency-step:hover {
      transform: translateY(-5px);
    }

    .emergency-step::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 4px;
      background: linear-gradient(90deg, var(--gradient-start), var(--gradient-end));
    }

    .step-header {
      display: flex;
      align-items: center;
      margin-bottom: 1.5rem;
    }

    .step-number {
      width: 40px;
      height: 40px;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      color: white;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      margin-right: 1rem;
    }

    .step-title {
      font-size: 1.5rem;
      color: var(--text);
      margin: 0;
    }

    .emergency-list {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    .emergency-list li {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
      padding: 0.8rem;
      background: rgba(37, 99, 235, 0.05);
      border-radius: 0.5rem;
      transition: transform 0.2s ease;
    }

    .emergency-list li:hover {
      transform: translateX(5px);
    }

    .emergency-list i {
      color: var(--primary);
      margin-right: 1rem;
      font-size: 1.2rem;
    }

    .contact-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
      margin: 2rem 0;
    }

    .contact-card {
      background: white;
      padding: 1.5rem;
      border-radius: 1rem;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      display: flex;
      align-items: center;
      transition: transform 0.3s ease;
    }

    .contact-card:hover {
      transform: translateY(-5px);
    }

    .contact-icon {
      width: 50px;
      height: 50px;
      background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 1rem;
    }

    .contact-icon i {
      color: white;
      font-size: 1.5rem;
    }

    .contact-info h4 {
      margin: 0 0 0.5rem 0;
      color: var(--text);
    }

    .contact-info p {
      margin: 0;
      color: var(--secondary);
    }

    .warning-container {
      background: linear-gradient(135deg, #fff5f5 0%, #ffe4e4 100%);
      border-radius: 1rem;
      padding: 2rem;
      margin: 2rem 0;
      position: relative;
      overflow: hidden;
    }

    .warning-header {
      display: flex;
      align-items: center;
      margin-bottom: 1.5rem;
      color: #dc2626;
    }

    .warning-header i {
      font-size: 2rem;
      margin-right: 1rem;
    }

    .warning-header h3 {
      margin: 0;
      font-size: 1.8rem;
    }

    .warning-list {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
    }

    .warning-item {
      display: flex;
      align-items: center;
      padding: 1rem;
      background: rgba(220, 38, 38, 0.1);
      border-radius: 0.5rem;
      transition: transform 0.2s ease;
    }

    .warning-item:hover {
      transform: translateX(5px);
    }

    .warning-item i {
      color: #dc2626;
      margin-right: 1rem;
      font-size: 1.2rem;
    }
  </style>
</head>
<body>
  <header>
    <div class="hero-content">
      <h1 class="hero-title">智慧支付・安心生活</h1>
      <p class="hero-subtitle">掌握行動支付安全，享受便利無憂的數位生活</p>
    </div>
    <img src="https://images.pexels.com/photos/230544/pexels-photo-230544.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="行動支付安全" class="hero-image">
  </header>

  <main>
    <nav>
      <button onclick="showSection('overview')" class="active">
        <i class="fas fa-home"></i> 概覽導覽
      </button>
      <button onclick="showSection('daily-security')">
        <i class="fas fa-shield-alt"></i> 日常防護
      </button>
      <button onclick="showSection('emergency')">
        <i class="fas fa-exclamation-circle"></i> 緊急應變
      </button>
      <button onclick="showSection('tech-protection')">
        <i class="fas fa-microchip"></i> 技術防護
      </button>
      <button onclick="showSection('enterprise')">
        <i class="fas fa-building"></i> 企業安全
      </button>
      <button onclick="showSection('sources')">
        <i class="fas fa-book"></i> 資料來源
      </button>
    </nav>

    <section id="overview">
      <div class="section-title">
        <h2>智慧支付新時代</h2>
        <p>掌握行動支付安全，享受便利無憂的數位生活</p>
      </div>

      <div class="content-block">
        <h3>行動支付安全重點</h3>
        <div class="feature-list">
          <div class="feature-list-item">
            <i class="fas fa-shield-alt"></i>
            <div>
              <h4>交易安全與個資保護</h4>
              <ul class="important-list">
                <li>動態交易密碼</li>
                <li>單次驗證代碼</li>
                <li>加密傳輸機制</li>
                <li>個資去識別化</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-mobile-alt"></i>
            <div>
              <h4>裝置安全與防盜機制</h4>
              <ul class="important-list">
                <li>生物辨識驗證</li>
                <li>遠端停用功能</li>
                <li>異常登入偵測</li>
                <li>裝置綁定機制</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-user-shield"></i>
            <div>
              <h4>詐騙防範與風險控管</h4>
              <ul class="important-list">
                <li>交易行為分析</li>
                <li>風險評分機制</li>
                <li>異常交易通報</li>
                <li>即時監控系統</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="content-block">
        <h3>支付方式比較</h3>
        <table class="comparison-table">
          <tr>
            <th>比較項目</th>
            <th>行動支付</th>
            <th>實體信用卡</th>
            <th>現金支付</th>
          </tr>
          <tr>
            <td>交易安全</td>
            <td>
              <span class="highlight"><i class="fas fa-shield-alt"></i>動態加密</span><br>
              <span class="highlight"><i class="fas fa-key"></i>單次交易代碼</span><br>
              <span class="highlight"><i class="fas fa-fingerprint"></i>生物辨識</span>
            </td>
            <td>
              <i class="fas fa-lock"></i>固定卡號與安全碼<br>
              <i class="fas fa-signature"></i>簽名驗證
            </td>
            <td>
              <i class="fas fa-money-bill"></i>實體交付<br>
              <i class="fas fa-eye"></i>當面點清
            </td>
          </tr>
          <tr>
            <td>使用便利性</td>
            <td>
              <span class="advantage"><i class="fas fa-check"></i>快速感應支付</span><br>
              <span class="disadvantage"><i class="fas fa-times"></i>需網路連線</span><br>
              <span class="disadvantage"><i class="fas fa-battery-quarter"></i>受電量限制</span>
            </td>
            <td>
              <span class="advantage"><i class="fas fa-check"></i>廣泛通用</span><br>
              <span class="advantage"><i class="fas fa-check"></i>無需網路</span><br>
              <span class="disadvantage"><i class="fas fa-times"></i>需實體攜帶</span>
            </td>
            <td>
              <span class="advantage"><i class="fas fa-check"></i>無使用限制</span><br>
              <span class="disadvantage"><i class="fas fa-times"></i>需準備零錢</span><br>
              <span class="disadvantage"><i class="fas fa-times"></i>攜帶不便</span>
            </td>
          </tr>
          <tr>
            <td>風險控管</td>
            <td>
              <span class="highlight"><i class="fas fa-shield-alt"></i>即時交易通知</span><br>
              <span class="highlight"><i class="fas fa-ban"></i>遠端停用功能</span><br>
              <span class="highlight"><i class="fas fa-chart-line"></i>交易行為分析</span>
            </td>
            <td>
              <i class="fas fa-phone"></i>電話掛失<br>
              <i class="fas fa-clock"></i>處理時間較長<br>
              <i class="fas fa-exclamation-triangle"></i>盜刷風險較高
            </td>
            <td>
              <i class="fas fa-exclamation-circle"></i>遺失無法追回<br>
              <i class="fas fa-search"></i>難以追蹤流向<br>
              <i class="fas fa-money-bill-wave"></i>攜帶風險高
            </td>
          </tr>
          <tr>
            <td>交易紀錄</td>
            <td>
              <span class="highlight"><i class="fas fa-history"></i>完整電子紀錄</span><br>
              <span class="highlight"><i class="fas fa-chart-bar"></i>消費分析功能</span><br>
              <span class="highlight"><i class="fas fa-file-invoice"></i>自動對帳</span>
            </td>
            <td>
              <i class="fas fa-receipt"></i>月結帳單<br>
              <i class="fas fa-search"></i>可查詢紀錄<br>
              <i class="fas fa-history"></i>資料較完整
            </td>
            <td>
              <i class="fas fa-receipt"></i>需保存單據<br>
              <i class="fas fa-times"></i>無電子紀錄<br>
              <i class="fas fa-calculator"></i>需手動記帳
            </td>
          </tr>
          <tr>
            <td>其他功能</td>
            <td>
              <span class="highlight"><i class="fas fa-gift"></i>整合優惠方案</span><br>
              <span class="highlight"><i class="fas fa-coins"></i>點數回饋</span><br>
              <span class="highlight"><i class="fas fa-chart-pie"></i>消費分析</span>
            </td>
            <td>
              <i class="fas fa-gift"></i>信用卡優惠<br>
              <i class="fas fa-coins"></i>紅利點數<br>
              <i class="fas fa-plane"></i>保險服務
            </td>
            <td>
              <i class="fas fa-times"></i>無附加功能<br>
              <i class="fas fa-times"></i>無優惠方案<br>
              <i class="fas fa-times"></i>無額外服務
            </td>
          </tr>
        </table>
      </div>

      <div class="image-showcase">
        <div class="showcase-item">
          <img src="https://images.pexels.com/photos/6347720/pexels-photo-6347720.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="生物辨識安全">
          <div class="showcase-content">
            <h3>生物辨識技術</h3>
            <p>多重身份驗證，確保交易安全</p>
          </div>
        </div>
        <div class="showcase-item">
          <img src="https://images.pexels.com/photos/5473298/pexels-photo-5473298.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="智慧監控">
          <div class="showcase-content">
            <h3>智慧監控系統</h3>
            <p>24小時全天候安全防護</p>
          </div>
        </div>
        <div class="showcase-item">
          <img src="https://images.pexels.com/photos/8353802/pexels-photo-8353802.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="加密技術">
          <div class="showcase-content">
            <h3>加密防護</h3>
            <p>先進的加密技術保護</p>
          </div>
        </div>
      </div>
    </section>

    <section id="daily-security">
      <div class="section-title">
        <h2>日常安全防護指南</h2>
        <p>建立安全的支付習慣，預防潛在風險</p>
      </div>

      <div class="content-block">
        <h3>風險預防重點</h3>
        <div class="grid-container">
          <div class="icon-card">
            <i class="fas fa-exclamation-triangle"></i>
            <h3>常見詐騙手法</h3>
            <ul class="important-list">
              <li>假冒銀行簡訊詐騙</li>
              <li>釣魚網站盜刷</li>
              <li>社交工程詐騙</li>
              <li>惡意程式入侵</li>
              <li>假冒客服詐騙</li>
              <li>盜刷卡號詐騙</li>
            </ul>
          </div>

          <div class="icon-card">
            <i class="fas fa-shield-alt"></i>
            <h3>防護建議</h3>
            <ul class="important-list">
              <li>定期更新密碼</li>
              <li>開啟雙重認證</li>
              <li>安裝防毒軟體</li>
              <li>避免使用公共Wi-Fi</li>
              <li>確認網站安全性</li>
              <li>保護個人資料</li>
            </ul>
          </div>

          <div class="icon-card">
            <i class="fas fa-check-circle"></i>
            <h3>安全使用準則</h3>
            <ul class="important-list">
              <li>確認商家資訊</li>
              <li>檢查交易明細</li>
              <li>保管裝置安全</li>
              <li>注意環境安全</li>
              <li>謹慎處理驗證碼</li>
              <li>定期檢查帳戶</li>
            </ul>
          </div>
        </div>
      </div>

      <div class="content-block">
        <h3>智慧防護措施</h3>
        <div class="feature-list">
          <div class="feature-list-item">
            <i class="fas fa-radar"></i>
            <div>
              <h4>智慧偵測・全天候監控</h4>
              <ul class="important-list">
                <li><span class="highlight">異地交易即時通知</span></li>
                <li><span class="highlight">大額交易主動確認</span></li>
                <li>異常時段提醒</li>
                <li>連續交易警示</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-brain"></i>
            <div>
              <h4>AI防護・精準預警</h4>
              <ul class="important-list">
                <li><span class="highlight">消費模式分析</span></li>
                <li><span class="highlight">風險評分預測</span></li>
                <li>行為軌跡比對</li>
                <li>詐騙模式識別</li>
              </ul>
            </div>
          </div>
        </div>
        <img src="https://images.pexels.com/photos/8370752/pexels-photo-8370752.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="安全防護" class="feature-image">
      </div>

      <div class="image-grid">
        <div class="image-card">
          <img src="https://images.pexels.com/photos/5473955/pexels-photo-5473955.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="密碼安全">
          <div class="card-content">
            <h3>密碼安全</h3>
            <p>定期更新，確保帳戶安全</p>
          </div>
        </div>
        <div class="image-card">
          <img src="https://images.pexels.com/photos/6963944/pexels-photo-6963944.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="雙重認證">
          <div class="card-content">
            <h3>雙重認證</h3>
            <p>多重防護，安全無虞</p>
          </div>
        </div>
        <div class="image-card">
          <img src="https://images.pexels.com/photos/5240544/pexels-photo-5240544.jpeg?auto=compress&cs=tinysrgb&w=1200" alt="資料加密">
          <div class="card-content">
            <h3>資料加密</h3>
            <p>先進加密，保護隱私</p>
          </div>
        </div>
      </div>
    </section>

    <section id="emergency">
      <div class="section-title">
        <h2>緊急應變處理</h2>
        <p>快速有效的緊急處理流程與注意事項</p>
      </div>

      <div class="emergency-flow">
        <div class="emergency-step">
          <div class="step-header">
            <div class="step-number">1</div>
            <h3 class="step-title">立即通報</h3>
          </div>
          <ul class="emergency-list">
            <li>
              <i class="fas fa-phone-alt"></i>
              <span>撥打緊急專線 165</span>
            </li>
            <li>
              <i class="fas fa-university"></i>
              <span>聯絡發卡銀行停卡</span>
            </li>
            <li>
              <i class="fas fa-shield-alt"></i>
              <span>通知資安單位處理</span>
            </li>
            <li>
              <i class="fas fa-file-alt"></i>
              <span>保留相關證據紀錄</span>
            </li>
            <li>
              <i class="fas fa-camera"></i>
              <span>截圖可疑交易資訊</span>
            </li>
          </ul>
        </div>

        <div class="emergency-step">
          <div class="step-header">
            <div class="step-number">2</div>
            <h3 class="step-title">帳戶控管</h3>
          </div>
          <ul class="emergency-list">
            <li>
              <i class="fas fa-lock"></i>
              <span>凍結支付功能</span>
            </li>
            <li>
              <i class="fas fa-power-off"></i>
              <span>停用相關服務</span>
            </li>
            <li>
              <i class="fas fa-key"></i>
              <span>變更重要密碼</span>
            </li>
            <li>
              <i class="fas fa-sliders-h"></i>
              <span>設定交易限制</span>
            </li>
            <li>
              <i class="fas fa-user-lock"></i>
              <span>啟動安全模式</span>
            </li>
          </ul>
        </div>

        <div class="emergency-step">
          <div class="step-header">
            <div class="step-number">3</div>
            <h3 class="step-title">安全檢查</h3>
          </div>
          <ul class="emergency-list">
            <li>
              <i class="fas fa-search"></i>
              <span>檢視交易紀錄</span>
            </li>
            <li>
              <i class="fas fa-virus-slash"></i>
              <span>掃描惡意程式</span>
            </li>
            <li>
              <i class="fas fa-mobile-alt"></i>
              <span>確認裝置安全</span>
            </li>
            <li>
              <i class="fas fa-cog"></i>
              <span>更新安全設定</span>
            </li>
            <li>
              <i class="fas fa-shield-virus"></i>
              <span>執行完整掃描</span>
            </li>
          </ul>
        </div>
      </div>

      <div class="contact-grid">
        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-phone-alt"></i>
          </div>
          <div class="contact-info">
            <h4>詐騙諮詢專線</h4>
            <p>165（24小時服務）</p>
          </div>
        </div>

        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-credit-card"></i>
          </div>
          <div class="contact-info">
            <h4>信用卡掛失專線</h4>
            <p>請參考各發卡銀行</p>
          </div>
        </div>

        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-comments"></i>
          </div>
          <div class="contact-info">
            <h4>金融消費評議中心</h4>
            <p>(02)2316-1288</p>
          </div>
        </div>

        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-envelope"></i>
          </div>
          <div class="contact-info">
            <h4>檢舉信箱</h4>
            <p>165@mail.moj.gov.tw</p>
          </div>
        </div>
      </div>

      <div class="warning-container">
        <div class="warning-header">
          <i class="fas fa-exclamation-triangle"></i>
          <h3>重要提醒</h3>
        </div>
        <div class="warning-list">
          <div class="warning-item">
            <i class="fas fa-check-circle"></i>
            <span>保持冷靜，依照步驟處理</span>
          </div>
          <div class="warning-item">
            <i class="fas fa-database"></i>
            <span>保留所有交易紀錄</span>
          </div>
          <div class="warning-item">
            <i class="fas fa-camera"></i>
            <span>截圖保存可疑內容</span>
          </div>
          <div class="warning-item">
            <i class="fas fa-wifi-slash"></i>
            <span>避免使用不安全網路</span>
          </div>
          <div class="warning-item">
            <i class="fas fa-user-shield"></i>
            <span>謹慎處理個人資料</span>
          </div>
          <div class="warning-item">
            <i class="fas fa-clock"></i>
            <span>及時通報相關單位</span>
          </div>
        </div>
      </div>
    </section>

    <section id="tech-protection">
      <div class="section-title">
        <h2>技術防護措施</h2>
        <p>多重技術防護機制，全方位保障交易安全</p>
      </div>

      <div class="grid-container">
        <div class="icon-card">
          <i class="fas fa-fingerprint"></i>
          <h3>生物辨識技術</h3>
          <ul class="important-list">
            <li>指紋辨識驗證</li>
            <li>臉部特徵辨識</li>
            <li>虹膜掃描技術</li>
            <li>聲紋比對系統</li>
            <li>行為模式辨識</li>
            <li>多重因素驗證</li>
          </ul>
        </div>

        <div class="icon-card">
          <i class="fas fa-shield-alt"></i>
          <h3>加密防護</h3>
          <ul class="important-list">
            <li>端對端加密傳輸</li>
            <li>SSL/TLS 安全協議</li>
            <li>資料加密存儲</li>
            <li>金鑰管理系統</li>
            <li>數位簽章技術</li>
            <li>區塊鏈防護</li>
          </ul>
        </div>

        <div class="icon-card">
          <i class="fas fa-brain"></i>
          <h3>AI 智慧防護</h3>
          <ul class="important-list">
            <li>行為模式分析</li>
            <li>異常交易偵測</li>
            <li>風險評分預測</li>
            <li>自動防護措施</li>
            <li>深度學習模型</li>
            <li>即時威脅偵測</li>
          </ul>
        </div>
      </div>

      <div class="content-block">
        <h3>新興防護技術</h3>
        <div class="feature-list">
          <div class="feature-list-item">
            <i class="fas fa-lock"></i>
            <div>
              <h4>量子加密技術</h4>
              <ul class="important-list">
                <li>量子金鑰分配</li>
                <li>後量子密碼學</li>
                <li>量子隨機數生成</li>
                <li>量子通訊協議</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-cube"></i>
            <div>
              <h4>區塊鏈安全</h4>
              <ul class="important-list">
                <li>智能合約驗證</li>
                <li>分散式帳本</li>
                <li>共識機制保護</li>
                <li>防篡改技術</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-network-wired"></i>
            <div>
              <h4>零信任架構</h4>
              <ul class="important-list">
                <li>身份驗證管理</li>
                <li>最小權限原則</li>
                <li>持續性監控</li>
                <li>動態存取控制</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="enterprise">
      <div class="section-title">
        <h2>企業安全管理</h2>
        <p>全方位的企業資安管理架構</p>
      </div>

      <div class="grid-container">
        <div class="icon-card">
          <i class="fas fa-users-cog"></i>
          <h3>人員管理</h3>
          <ul class="important-list">
            <li>定期安全培訓</li>
            <li>權限分級管理</li>
            <li>行為準則制定</li>
            <li>意外事件通報</li>
            <li>資安意識教育</li>
            <li>社交工程演練</li>
          </ul>
        </div>

        <div class="icon-card">
          <i class="fas fa-tasks"></i>
          <h3>流程管控</h3>
          <ul class="important-list">
            <li>標準作業程序</li>
            <li>風險評估機制</li>
            <li>定期稽核檢查</li>
            <li>改善追蹤管理</li>
            <li>事件應變流程</li>
            <li>合規性稽核</li>
          </ul>
        </div>

        <div class="icon-card">
          <i class="fas fa-shield-virus"></i>
          <h3>技術防護</h3>
          <ul class="important-list">
            <li>防火牆部署</li>
            <li>入侵偵測系統</li>
            <li>弱點掃描</li>
            <li>資安監控中心</li>
            <li>端點防護</li>
            <li>加密通訊</li>
          </ul>
        </div>
      </div>

      <div class="content-block">
        <h3>企業資安架構</h3>
        <div class="feature-list">
          <div class="feature-list-item">
            <i class="fas fa-shield-alt"></i>
            <div>
              <h4>零信任架構</h4>
              <ul class="important-list">
                <li>身份驗證管理</li>
                <li>存取控制機制</li>
                <li>網路分段管理</li>
                <li>加密通訊協定</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-user-shield"></i>
            <div>
              <h4>身份管理</h4>
              <ul class="important-list">
                <li>多因素認證</li>
                <li>權限分級制度</li>
                <li>存取紀錄追蹤</li>
                <li>帳號生命週期</li>
              </ul>
            </div>
          </div>
          <div class="feature-list-item">
            <i class="fas fa-network-wired"></i>
            <div>
              <h4>網路安全</h4>
              <ul class="important-list">
                <li>網路分段隔離</li>
                <li>流量監控分析</li>
                <li>異常行為偵測</li>
                <li>安全通訊協定</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="stats-container">
          <div class="stat-item">
            <div class="stat-number">99.9%</div>
            <div class="stat-label">系統可用性</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">24/7</div>
            <div class="stat-label">全天候監控</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">&lt;1ms</div>
            <div class="stat-label">響應時間</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">100%</div>
            <div class="stat-label">加密保護</div>
          </div>
        </div>
      </div>
    </section>

    <section id="sources">
      <div class="section-title">
        <h2>參考資料與來源</h2>
        <p>本網站內容參考自權威機構與專業組織</p>
      </div>

      <div class="content-block">
        <div class="source-grid">
          <div class="source-category">
            <h3>技術標準與規範</h3>
            <ul class="source-list">
              <li>
                <i class="fas fa-book"></i>
                <a href="https://www.pcisecuritystandards.org/" target="_blank">PCI DSS 支付卡產業資料安全標準</a>
                <p>支付卡產業資料安全標準，確保支付卡資料的安全</p>
              </li>
              <li>
                <i class="fas fa-shield-alt"></i>
                <a href="https://www.nist.gov/cyberframework" target="_blank">NIST 網路安全框架</a>
                <p>美國國家標準與技術研究院制定的網路安全框架</p>
              </li>
              <li>
                <i class="fas fa-lock"></i>
                <a href="https://www.iso.org/isoiec-27001-information-security.html" target="_blank">ISO 27001 資訊安全管理</a>
                <p>國際標準化組織的資訊安全管理系統標準</p>
              </li>
              <li>
                <i class="fas fa-shield-alt"></i>
                <a href="https://www.fsc.gov.tw/" target="_blank">金融監督管理委員會</a>
                <p>台灣金融監理機構制定的電子支付相關規範</p>
              </li>
            </ul>
          </div>

          <div class="source-category">
            <h3>支付安全技術</h3>
            <ul class="source-list">
              <li>
                <i class="fas fa-credit-card"></i>
                <a href="https://usa.visa.com/partner-with-us/payment-technology/visa-token-service.html" target="_blank">Visa Token 服務</a>
                <p>Visa 的代碼化支付安全技術</p>
              </li>
              <li>
                <i class="fab fa-apple"></i>
                <a href="https://support.apple.com/en-us/HT203027" target="_blank">Apple Pay 安全機制</a>
                <p>Apple Pay 的安全設計與防護機制</p>
              </li>
              <li>
                <i class="fab fa-google"></i>
                <a href="https://support.google.com/pay/answer/7644139" target="_blank">Google Pay 安全防護</a>
                <p>Google Pay 的安全功能與保護措施</p>
              </li>
              <li>
                <i class="fas fa-mobile-alt"></i>
                <a href="https://www.samsung.com/tw/apps/samsung-pay/security/" target="_blank">Samsung Pay 安全技術</a>
                <p>Samsung Pay 的安全技術與防護方案</p>
              </li>
            </ul>
          </div>

          <div class="source-category">
            <h3>研究報告與白皮書</h3>
            <ul class="source-list">
              <li>
                <i class="fas fa-file-alt"></i>
                <a href="https://www.mckinsey.com/" target="_blank">McKinsey 行動支付研究報告</a>
                <p>全球行動支付發展趨勢與安全分析</p>
              </li>
              <li>
                <i class="fas fa-chart-line"></i>
                <a href="https://www.gartner.com/" target="_blank">Gartner 支付安全分析</a>
                <p>支付安全技術發展與市場趨勢報告</p>
              </li>
              <li>
                <i class="fas fa-university"></i>
                <a href="https://www.bis.org/" target="_blank">國際清算銀行研究</a>
                <p>國際支付系統安全標準與規範</p>
              </li>
            </ul>
          </div>

          <div class="source-category">
            <h3>緊急聯絡資訊</h3>
            <ul class="source-list">
              <li>
                <i class="fas fa-phone"></i>
                <span>金融詐騙諮詢專線：165</span>
                <p>24小時免付費諮詢服務</p>
              </li>
              <li>
                <i class="fas fa-credit-card"></i>
                <span>信用卡掛失：請參考各發卡銀行</span>
                <p>建議將重要掛失電話儲存於通訊錄</p>
              </li>
              <li>
                <i class="fas fa-envelope"></i>
                <span>網路犯罪檢舉：165@mail.moj.gov.tw</span>
                <p>提供網路詐騙案件檢舉管道</p>
              </li>
              <li>
                <i class="fas fa-comments"></i>
                <span>金融消費評議中心：(02)2316-1288</span>
                <p>金融消費爭議處理與諮詢</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <footer>
      <div class="footer-content">
        <div class="footer-section">
          <h3>關於我們</h3>
          <p>致力於提供最新、最完整的行動支付安全資訊，協助使用者建立安全的支付環境。</p>
        </div>
        <div class="footer-section">
          <h3>聯絡資訊</h3>
          <ul>
            <li><i class="fas fa-envelope"></i> contact@mobilepay-security.com</li>
            <li><i class="fas fa-phone"></i> (02) 2345-6789</li>
            <li><i class="fas fa-map-marker-alt"></i> 台北市信義區信義路五段7號</li>
          </ul>
        </div>
        <div class="footer-section">
          <h3>追蹤我們</h3>
          <div class="social-links">
            <a href="#"><i class="fab fa-facebook"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-linkedin"></i></a>
            <a href="#"><i class="fab fa-youtube"></i></a>
          </div>
        </div>
      </div>
      <p class="copyright">&copy; 2025 行動支付資安總覽 版權所有</p>
    </footer>
  </main>

  <script>
    function showSection(id) {
      document.querySelectorAll("nav button").forEach(btn => {
        btn.classList.remove("active");
      });
      
      document.querySelector(`button[onclick="showSection('${id}')"]`).classList.add("active");
      
      document.querySelectorAll("section").forEach(sec => {
        sec.classList.remove("active");
        sec.style.opacity = "0";
        sec.style.transform = "translateY(20px)";
      });

      const targetSection = document.getElementById(id);
      targetSection.classList.add("active");
      setTimeout(() => {
        targetSection.style.opacity = "1";
        targetSection.style.transform = "translateY(0)";
      }, 100);
    }

    document.addEventListener('DOMContentLoaded', () => {
      document.querySelector('nav button').classList.add('active');
      showSection('overview');
    });
  </script>
</body>
</html> 
