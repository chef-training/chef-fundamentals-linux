#
# Rake tasks for building, managing, and packaging the ChefDK-Fundamentals
#

# This is provides quick-and-dirty support for the metadata file within this project
def name(value = nil) ; value ? @name = value : @name ; end
def maintainer(value = nil) ; value ? @maintainer = value : @maintainer ; end
def maintainer_email(value = nil) ; value ? @maintainer_email = value : @maintainer_email ; end
def license(value = nil) ; value ? @license = value : @license ; end
def description(value = nil) ; value ? @description = value : @description ; end
def version(value = nil) ; value ? @version = value : @version ; end

def local_release_folder(value = nil) ; value ? @local_release_folder = value : @local_release_folder ; end

def asset(filename,*params) ; assets << filename ; end
def assets ; @assets ||= [] ; end

def archive_filename
  "#{name}-#{version}.zip"
end

def clean_command
  "rm #{archive_filename}"
end

def archive_command
  "zip #{archive_filename} #{ assets.join(" ") }"
end

def copy_command
  "cp #{archive_filename} #{local_release_folder}/#{archive_filename}"
end

instance_eval(File.read("metadata.rb"))

task :default => :release

task :clean do
  `#{clean_command}`
end

task :package do
  `#{archive_command}`
end

task :release => :package do
  puts %{
********************************************************************************

  Copying to Google Drive Location

  > Unfortunately right now this is hard-coded to where you have Google Drive
  > syncronized locally. In the future it would be great to use some Google
  > auth to allow for this new release to be created.

********************************************************************************
}

  puts copy_command
  `#{copy_command}`
end
