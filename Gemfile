source "https://rubygems.org"
  gem "github-pages", group: :jekyll_plugins
  gem "autoprefixer-rails"
  gem "jekyll-assets"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-sitemap"
  gem "jekyll-redirect-from"
  gem "jekyll-seo-tag"
end

install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?

