package javalab;

import java.util.*;

abstract class Member {
    protected String memberId;
    protected String name;
    protected String email;
    protected String tier;
    protected int milesBalance;

    public Member(String memberId, String name, String email) {
        this.memberId = memberId;
        this.name = name;
        this.email = email;
        this.tier = "Silver"; // default
        this.milesBalance = 0;
    }

    
    public String getMemberId() { return memberId; }
    public String getName() { return name; }
    public String getEmail() { return email; }
    public String getTier() { return tier; }
    public int getMilesBalance() { return milesBalance; }

    public void setTier(String tier) { this.tier = tier; }
    protected void setMilesBalance(int miles) { this.milesBalance = miles; }

    // Credit miles (Overloading)
    public void creditMiles(int distance) {
        milesBalance += (int)(distance * getBonusMultiplier());
    }

    public void creditMiles(int distance, String fareClass) {
        int bonus = fareClass.equalsIgnoreCase("Business") ? 2 : 1;
        milesBalance += (int)(distance * bonus * getBonusMultiplier());
    }

    // Abstract methods for tier handling
    public abstract double getBonusMultiplier();
    public abstract void evaluateTier();

    // Statement
    public void printStatement() {
        System.out.println("---- Statement ----");
        System.out.println("ID: " + memberId + " | Name: " + name);
        System.out.println("Tier: " + tier + " | Miles: " + milesBalance);
    }
}

// Silver Member
class SilverMember extends Member {
    public SilverMember(String memberId, String name, String email) {
        super(memberId, name, email);
        this.tier = "Silver";
    }

    @Override
    public double getBonusMultiplier() { return 1.0; }

    @Override
    public void evaluateTier() {
        if (milesBalance >= 25000) {
            setTier("Gold");
        }
    }
}

// Gold Member
class GoldMember extends Member {
    public GoldMember(String memberId, String name, String email) {
        super(memberId, name, email);
        this.tier = "Gold";
    }

    @Override
    public double getBonusMultiplier() { return 1.25; }

    @Override
    public void evaluateTier() {
        if (milesBalance >= 50000) {
            setTier("Platinum");
        }
    }
}


class PlatinumMember extends Member {
    public PlatinumMember(String memberId, String name, String email) {
        super(memberId, name, email);
        this.tier = "Platinum";
    }

    @Override
    public double getBonusMultiplier() { return 1.5; }

    @Override
    public void evaluateTier() {
        
    }
}
