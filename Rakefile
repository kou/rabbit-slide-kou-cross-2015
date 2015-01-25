require "rabbit/task/slide"

# Edit ./config.yaml to customize meta data

spec = nil
Rabbit::Task::Slide.new do |task|
  spec = task.spec
  spec.files += Dir.glob("*.svg")
  spec.files += Dir.glob("images/*.svg")
  # spec.files -= Dir.glob("private/**/*.*")
  spec.add_runtime_dependency("rabbit-slide-groonga")
end

desc "Tag #{spec.version}"
task :tag do
  sh("git", "tag", "-a", spec.version.to_s, "-m", "Publish #{spec.version}")
  sh("git", "push", "--tags")
end

rule ".pdf" => ".svg" do |task|
  sh("inkscape", "--export-pdf", task.name, task.source)
end

desc "Generate self introduction slide"
task "self-introduction" => "self-introduction.pdf"
