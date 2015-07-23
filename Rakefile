task :publish => :build do
  sh 'if [[ $(git status -s) ]]; then git add -A . && git commit; fi'
  Dir.chdir('_site') do
    sh 'git init'
    sh 'git add .'
    sh 'git commit -m "Published website"'
    sh 'git remote add origin git@github.com:jwilger/jwilger.github.com.git; true'
    sh 'git push -fu origin master'
  end
end

task :build do
  sh 'jekyll b'
end
