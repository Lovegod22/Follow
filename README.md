require 'bcrypt'
class User < ApplicationRecord
    has_secure_password

    has_many :followed_users, foreign_key: :follower_id, class_name: 'Follow'
    has_many :followees, through: :followed_users
    has_many :following_users, foreign_key: :followee_id, class_name: 'Follow'
    has_many :followers, through: :following_users

    validates :user_name, uniqueness: { case_sensitive: true }
    validates :user_name, presence: true
    validates :name, presence: true
    validates :location, presence: true
    validates :bio, presence: true
end
