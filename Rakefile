# -*- ruby -*-

require "bundler/setup"
require "jekyll/task/i18n"

Jekyll::Task::I18n.define do |task|
  task.locales = ["ja"]
  task.files = Rake::FileList["**/*.md"]
  task.files -= Rake::FileList["_*/**/*.md"]
  task.locales.each do |locale|
    task.files -= Rake::FileList["#{locale}/**/*.md"]
  end
  task.custom_translator = lambda do |original, translated, path|
    notice = <<-NOTICE
{% comment %}
##############################################
  THIS FILE IS AUTOMATICALLY GENERATED FROM
  "#{path.po_file}"
  DO NOT EDIT THIS FILE MANUALLY!
##############################################
{% endcomment %}
    NOTICE
    if /^---+$/ =~ translated
      translated = translated.split(/^---+\n/)
      translated[2] = "\n#{notice}\n#{translated[2]}"
      translated.join("---\n")
    else
      "\n#{notice}\n#{translated}"
    end
  end
end

task :default => "jekyll:i18n:translate"
