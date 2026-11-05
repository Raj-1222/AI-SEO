# Aurify AI SEO Automation Platform

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![PHP](https://img.shields.io/badge/PHP-7.4%2B-purple.svg)
![MySQL](https://img.shields.io/badge/MySQL-5.7%2B-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

A comprehensive, AI-powered SEO automation platform that helps you optimize websites, generate content, analyze competitors, and improve search engine rankings with cutting-edge artificial intelligence.

## 🚀 Features

### Core SEO Tools
- **🔍 Website Audit** - Complete technical SEO analysis with actionable recommendations
- **⚡ PageSpeed Insights** - Real-time performance analysis and optimization suggestions
- **🎯 Keyword Generator** - AI-powered keyword research and analysis
- **📝 Meta Tag Generator** - Automated meta descriptions and title tags
- **🏷️ Schema Generator** - Structured data markup for better SERP visibility
- **🔗 Canonical Checker** - Detect and fix canonical URL issues

### AI-Powered Features
- **✍️ Blog Generator** - Generate SEO-optimized blog posts with AI
- **🤖 Gemini AI Integration** - Advanced content generation using Google's Gemini
- **💬 ChatGPT Integration** - OpenAI-powered content optimization
- **🔬 Competitor SEO Analysis** - In-depth competitor research and gap analysis

### Optimization Tools
- **🖼️ Image Optimizer** - Compress and optimize images for faster load times
- **📊 SEO Score Calculator** - Real-time SEO scoring and recommendations
- **📈 Technical SEO Analyzer** - Crawl issues, robots.txt, sitemap validation
- **📧 Email Reports** - Automated PDF reports sent to clients

### Integration & Automation
- **🔄 N8n Webhook Integration** - Automate workflows and connect with other tools
- **📱 RESTful API** - All features accessible via API endpoints
- **📊 Analytics Dashboard** - Real-time SEO metrics and performance tracking
- **📜 History Tracking** - Monitor SEO improvements over time

## 📋 Table of Contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Database Setup](#database-setup)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Features in Detail](#features-in-detail)
- [Project Structure](#project-structure)
- [Security](#security)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🛠️ Requirements

- **PHP**: 7.4 or higher
- **MySQL**: 5.7 or higher
- **Web Server**: Apache/Nginx with mod_rewrite enabled
- **PHP Extensions**:
  - mysqli
  - curl
  - json
  - gd or imagick (for image optimization)
  - mbstring
  - openssl

### External API Keys (Optional but Recommended)
- Google PageSpeed Insights API key
- OpenAI API key (for ChatGPT features)
- Google Gemini API key (for Gemini AI features)

## 📥 Installation

### ⚠️ IMPORTANT SECURITY NOTICE

**Before pushing to GitHub or deploying:**
1. Never commit `config/database.php` - it contains your credentials
2. The file is already in `.gitignore` for safety
3. Use `config/database.example.php` as a template
4. Keep API keys in environment variables or secure config files
5. See [SECURITY.md](SECURITY.md) for complete security guidelines

### Step 1: Clone or Download

```bash
git clone https://github.com/yourusername/ai-seo.git
cd ai-seo
```

### Step 2: Configure Database

1. Copy the example configuration:
```bash
cp config/database.example.php config/database.php
```

2. Edit `config/database.php` with your database credentials:
```php
define('DB_HOST', 'localhost');
define('DB_USER', 'your_username');
define('DB_PASS', 'your_password');
define('DB_NAME', 'aurify_seo');
```

### Step 3: Import Database Schema

Import all SQL files in the `database/` directory:

```bash
mysql -u your_username -p aurify_seo < database/schema.sql
mysql -u your_username -p aurify_seo < database/canonical_checker_schema.sql
mysql -u your_username -p aurify_seo < database/competitor_seo_schema.sql
mysql -u your_username -p aurify_seo < database/image_optimizer_schema.sql
```

Or use phpMyAdmin to import the SQL files.

### Step 4: Set Permissions

```bash
chmod 755 -R .
chmod 777 -R uploads/
chmod 777 -R logs/
```

### Step 5: Configure Web Server

#### Apache (.htaccess)
```apache
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    
    # Redirect to index.php
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ index.php [L,QSA]
</IfModule>
```

#### Nginx
```nginx
location / {
    try_files $uri $uri/ /index.php?$query_string;
}

location ~ \.php$ {
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    fastcgi_index index.php;
    include fastcgi_params;
}
```

## ⚙️ Configuration

### API Keys

Edit `config/init.php` or create environment variables:

```php
// Google PageSpeed API
define('PAGESPEED_API_KEY', 'your_google_api_key');

// OpenAI API
define('OPENAI_API_KEY', 'your_openai_api_key');

// Google Gemini API
define('GEMINI_API_KEY', 'your_gemini_api_key');

// Email Configuration
define('SMTP_HOST', 'smtp.example.com');
define('SMTP_PORT', 587);
define('SMTP_USER', 'your_email@example.com');
define('SMTP_PASS', 'your_email_password');
```

### Site Configuration

Edit theme colors and site settings in `config/database.php`:

```php
define('SITE_NAME', 'Aurify AI SEO Automation');
define('SITE_URL', 'https://yourdomain.com');
define('PRIMARY_COLOR', '#FF6B00');
define('SECONDARY_COLOR', '#0B1F4D');
```

## 🗄️ Database Setup

The platform uses MySQL database with the following main tables:

- `users` - User authentication and profiles
- `websites` - Website audit records
- `keywords` - Keyword tracking and analysis
- `audits` - SEO audit history
- `competitor_analysis` - Competitor SEO data
- `canonical_urls` - Canonical URL checks
- `image_optimizations` - Image optimization logs
- `seo_scores` - SEO score history

Default admin credentials after installation:
- **Email**: admin@aurify.com
- **Password**: admin123

⚠️ **Change these credentials immediately after first login!**

## 🎯 Usage

### Quick Start

1. **Login**: Navigate to `/views/auth/login.php`
2. **Dashboard**: View your SEO overview at `/views/dashboard/`
3. **Website Audit**: Go to Website Audit tool and enter a URL
4. **Generate Keywords**: Use the Keyword Generator for content research
5. **Optimize Images**: Upload images to the Image Optimizer
6. **Create Content**: Use the Blog Generator for AI-written articles

### Main Workflows

#### 1. Complete Website SEO Audit
```
Dashboard → Website Audit → Enter URL → Generate Report → Download PDF
```

#### 2. Competitor Analysis
```
Dashboard → Competitor SEO → Enter Competitor URLs → Analyze → View Gaps
```

#### 3. Content Generation
```
Dashboard → Blog Generator → Enter Topic → Generate → Edit → Export
```

#### 4. Image Optimization
```
Dashboard → Image Optimizer → Upload Images → Optimize → Download
```

## 📚 API Documentation

### Base URL
```
https://yourdomain.com/api/
```

### Authentication
Include session cookie or use API tokens (configure in settings).

### Available Endpoints

#### Website Audit
```http
POST /api/audit.php
Content-Type: application/json

{
  "url": "https://example.com",
  "user_id": 1
}
```

#### Keyword Generator
```http
POST /api/keyword-generator.php
Content-Type: application/json

{
  "seed_keyword": "seo tools",
  "count": 50
}
```

#### Meta Generator
```http
POST /api/meta-generator.php
Content-Type: application/json

{
  "url": "https://example.com",
  "content": "Page content here..."
}
```

#### Image Optimizer
```http
POST /api/image-optimizer.php
Content-Type: multipart/form-data

file: [binary image data]
quality: 85
format: webp
```

#### Competitor SEO Analysis
```http
POST /api/competitor-seo.php
Content-Type: application/json

{
  "urls": [
    "https://competitor1.com",
    "https://competitor2.com"
  ]
}
```

Full API documentation available at `/api/docs/` (if enabled).

## 🔧 Features in Detail

### Website Audit
Comprehensive SEO analysis including:
- Meta tags validation
- Heading structure analysis
- Image optimization check
- Mobile-friendliness
- Page speed metrics
- Security headers
- Broken links detection
- Schema markup validation

### AI Content Generation
- Blog post generation with custom tone and style
- Meta description optimization
- Title tag suggestions
- Content rewriting and improvement
- Keyword density optimization

### Image Optimizer
- Batch image compression
- Format conversion (JPEG, PNG, WebP)
- Dimension resizing
- Metadata stripping
- Before/after comparison
- Optimization history

### Competitor Analysis
- Backlink comparison
- Keyword gap analysis
- Content strategy insights
- Technical SEO comparison
- SERP position tracking

## 📁 Project Structure

```
ai-seo/
├── api/                      # API endpoints
│   ├── audit.php
│   ├── keyword-generator.php
│   ├── meta-generator.php
│   ├── image-optimizer.php
│   └── ...
├── assets/                   # Frontend assets
│   ├── css/
│   │   ├── style.css
│   │   ├── modern-ui.css
│   │   └── components.css
│   └── js/
│       ├── main.js
│       ├── audit.js
│       └── ...
├── config/                   # Configuration files
│   ├── database.php
│   ├── init.php
│   └── image_optimizer_config.php
├── controllers/              # Business logic
│   ├── AuditController.php
│   ├── AuthController.php
│   ├── BlogGeneratorController.php
│   └── ...
├── database/                 # SQL schemas
│   ├── schema.sql
│   ├── canonical_checker_schema.sql
│   └── ...
├── models/                   # Data models
├── services/                 # Service classes
├── views/                    # Frontend views
│   ├── auth/
│   ├── dashboard/
│   └── includes/
├── uploads/                  # User uploads
├── logs/                     # Application logs
├── index.php                 # Entry point
└── README.md                 # This file
```

## 🔒 Security

### Best Practices Implemented

- ✅ Password hashing with bcrypt
- ✅ SQL injection prevention with prepared statements
- ✅ XSS protection with input sanitization
- ✅ CSRF token validation
- ✅ Session security with regeneration
- ✅ Secure file upload validation
- ✅ Rate limiting on API endpoints
- ✅ HTTPS enforcement (configure in web server)

### Security Recommendations

1. **Change default credentials** immediately after installation
2. **Use HTTPS** in production environments
3. **Keep API keys** in environment variables, not in code
4. **Regular backups** of database and uploaded files
5. **Update PHP** and dependencies regularly
6. **Restrict file permissions** appropriately
7. **Enable error logging** but disable display_errors in production

## 🐛 Troubleshooting

### Common Issues

#### "Database connection failed"
- Check database credentials in `config/database.php`
- Verify MySQL service is running
- Ensure database exists and user has privileges

#### "API key invalid"
- Verify API keys are correctly set in configuration
- Check API key quotas and billing status
- Ensure no extra spaces in API key values

#### "Image upload failed"
- Check `uploads/` directory exists and is writable (chmod 777)
- Verify PHP `upload_max_filesize` and `post_max_size` settings
- Ensure GD or Imagick extension is installed

#### "Session expired immediately"
- Check session.save_path is writable
- Verify server time zone is set correctly
- Clear browser cookies and try again

#### "White page / 500 error"
- Check PHP error logs: `/var/log/php-error.log`
- View application logs: `/logs/error.log`
- Verify all required PHP extensions are installed

### Debug Mode

Enable debug mode in `config/init.php`:
```php
define('DEBUG_MODE', true);
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

⚠️ **Disable debug mode in production!**

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/YourFeature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/YourFeature`
5. Open a Pull Request

### Coding Standards
- Follow PSR-12 coding standards for PHP
- Use meaningful variable and function names
- Comment complex logic
- Write unit tests for new features

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Credits

Built with:
- PHP & MySQL
- OpenAI GPT API
- Google Gemini AI
- Google PageSpeed Insights API
- Chart.js for analytics
- Modern CSS Grid & Flexbox

## 📞 Support

For support and questions:
- **Email**: support@aurify.com
- **Documentation**: [https://docs.aurify.com](https://docs.aurify.com)
- **Issues**: [GitHub Issues](https://github.com/yourusername/ai-seo/issues)

## 🗺️ Roadmap

### Upcoming Features
- [ ] Multi-language support
- [ ] WordPress plugin integration
- [ ] Advanced A/B testing tools
- [ ] Voice search optimization
- [ ] Video SEO analysis
- [ ] Local SEO tools
- [ ] Social media integration
- [ ] Advanced competitor tracking

---

**Made with ❤️ by the Aurify Team**

*Last Updated: November 2026*
