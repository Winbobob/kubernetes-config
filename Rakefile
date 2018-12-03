task default: %i[lint package]

CHARTS = FileList["charts/*"].resolve

task :lint do
  CHARTS.each do |chart|
    sh "helm lint #{chart}"
  end
end

task :package do
  mkdir_p "dist"
  Dir.chdir "dist" do
    CHARTS.each do |chart|
      sh "helm package -u ../#{chart}"
    end
    sh "helm repo index . --url https://travis-ci-helm-charts.storage.googleapis.com"
  end
end
