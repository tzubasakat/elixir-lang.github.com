require 'bundler/setup'
require 'jekyll/task/i18n'

Jekyll::Task::I18n.define do |task|
  task.locales = ['ja']
  task.files = Rake::FileList["**/*.md", "**/*.html", "**/*.markdown", "**/*.yml"]
  task.files -= Rake::FileList["_site/**/*", "docs/**/*", "vendor/bundle/**/*", "README.md"]
  task.locales.each do |locale|
    task.files -= Rake::FileList["#{locale}/**/*.md", "#{locale}/**/*.html", "#{locale}/**/*.markdown", "#{locale}/**/*.yml"]
  end
end

task default: 'jekyll:i18n:translate'
