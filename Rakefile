#!env ruby
require 'rubygems'

require 'csv'
require 'pry'
require 'workable'

def api_config_set?
  ENV.has_key?('API_KEY') && ENV.has_key?('SUBDOMAIN')
end

task :default => ['planetargon:workable:export_candidates_from_archived_job_ads']

namespace :planetargon do
  namespace :workable do
    desc "Export all candidate data to a CSV"
    task :export_candidates_from_archived_job_ads do
      abort "API_KEY and/or SUBDOMAIN values are not found in .env" unless api_config_set?
      client = Workable::Client.new(api_key: ENV['API_KEY'], subdomain: ENV['SUBDOMAIN'])
      jobs = client.jobs

      # CSV headers
      headers = %w( job_title
                    candidate_first_name
                    candidate_last_name
                    candidate_email_address
                    applied_on
                    applied_on_friendly
                    address
                    profile_url
                    job_url )

      CSV.open("export/#{Time.now.strftime('%Y%m%d-%H%M')}-workable.csv", "w") do |csv|

        # Add headers to the first row
        csv << headers

        jobs.each do |job|
          # Only fetch candidates to Ruby on Rails job ads
          next unless job['title'] =~ /rails/i

          # Skip any internship positions
          next if job['title'] =~ /intern/i

          # Fetch all candidates for this particular job ad
          candidates = client.job_candidates(job['shortcode'])

          candidates.each do |candidate|
            # Skip any candidates that we ruled out
            next if candidate['disqualified'] == true

            # Skip if we hired them
            next unless candidate['hired_at'].nil?

            candidate_row = [ job['title'],
                              candidate['firstname'],
                              candidate['lastname'],
                              candidate['email'],
                              candidate['created_at'],
                               Date.parse(candidate['created_at']).strftime('%B of %Y'),
                              candidate['address'],
                              candidate['profile_url'],
                              job['url'] ]

            # puts candidate_row

            # Append these to the CSV file
            csv << candidate_row
          end
          sleep(5) # Avoiding hitting Workable's API rate limit
        end
      end
    end
  end
end
